

```java
// Fig. 31.20: Reservation.java
// Airline reservation web service.
package com.deitel.reservation;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import javax.annotation.Resource;
import javax.jws.WebMethod;
import javax.jws.WebParam;
import javax.jws.WebService;
import javax.sql.DataSource;

@WebService()
public class Reservation
{
    // allow the server to inject the DataSource
    @Resource( name="jdbc/reservation" )
    DataSource dataSource;

    // a WebMethod that can reserve a seat
    @WebMethod( operationName = "reserve" )
    public boolean reserve( @WebParam( name = "seatType" ) String seatType,
        @WebParam( name = "classType" ) String classType )
    {
        Connection connection = null;
        PreparedStatement lookupSeat = null;
        PreparedStatement reserveSeat = null;

        try
        {
            connection = DriverManager.getConnection(
                DATABASE_URL, USERNAME, PASSWORD );
            lookupSeat = connection.prepareStatement(
                "SELECT \"number\" FROM \"seats\" WHERE (\"taken\" = 0) " +
                "AND (\"location\" = ?) AND (\"class\" = ?)");
            lookupSeat.setString( 1, seatType );
            lookupSeat.setString( 2, classType );
            ResultSet resultSet = lookupSeat.executeQuery();

            // if requested seat is available, reserve it
            if ( resultSet.next() )
            {
                int seat = resultSet.getInt( 1 );
                reserveSeat = connection.prepareStatement(
                    "UPDATE \"seats\" SET \"taken\"=1 WHERE \"number\"=?" );
                reserveSeat.setInt( 1, seat );
                reserveSeat.executeUpdate();
                return true;
            } // end if
```

这将数据库中的座位标记为已占用。参数 number 被 seat 的值替换。方法 reserve 返回 true（第 49 行）以表示预订成功。如果没有匹配的座位，或发生异常，方法 reserve 返回 false（第 52、57、62 和 75 行）以表示没有座位匹配用户的请求。

## 31.10.2 创建一个与预订服务交互的 Web 应用程序

本节介绍一个 ReservationClient JSF Web 应用程序，该应用程序使用 Reservation Web 服务。应用程序允许用户选择 “Aisle”、“Middle” 或 “Window” 座位，以及 “Economy” 或 “First” 等舱，然后将请求提交给 Web 服务。如果数据库请求不成功，应用程序会指示用户修改请求并重试。这里介绍的应用程序是使用第 29–30 章介绍的技术构建的。我们假设您已经阅读了这些章节，因此知道如何构建一个 Facelets 页面和相应的 JavaBean。

### index.xhtml

index.xhtml（图 31.21）定义了两个 h:selectOneMenus 和一个 h:commandButton。第 16–20 行的 h:selectOneMenu 显示用户可以从中选择的全部座位类型。第 21–24 行的菜单提供舱位类型的选择。这些值的存储在 reservationBean（图 31.22）的 seatType 和 classType 属性中。用户在从 h:selectOneMenus 中做出选择后，点击 Reserve 按钮（第 25–26 行）以提交请求。点击按钮会调用 reservationBean 的 reserveSeat 方法。页面在第 28 行显示每次预订座位尝试的结果。

```html
1 <?xml version='1.0' encoding='UTF-8' ?>
2 
3 <!-- Fig. 31.21: index.xhtml -->
4 <!-- Facelets page that allows a user to select a seat -->
5 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
6 "http://www.w3.org/TR/xhtml11/DTD/xhtml11-transitional.dtd">
7 <html xmlns="http://www.w3.org/1999/xhtml"
8 xmlns:h="http://java.sun.com/jsf/html"
9 xmlns:f="http://java.sun.com/jsf/core">
10 <h:head>
11 <title>Airline Reservations</title>
12 </h:head>
13 <h:body>
14 <h:form>
15 <h3>Please select the seat type and class to reserve:</h3>
16 <h:selectOneMenu value="#{reservationBean.seatType}">
17 <f:selectItem itemValue="Aisle" itemLabel="Aisle" />
18 <f:selectItem itemValue="Middle" itemLabel="Middle" />
19 <f:selectItem itemValue="Window" itemLabel="Window" />
20 </h:selectOneMenu>
21 <h:selectOneMenu value="#{reservationBean.classType}">
22 <f:selectItem itemValue="Economy" itemLabel="Economy" />
23 <f:selectItem itemValue="First" itemLabel="First" />
24 </h:selectOneMenu>
25        <h:commandButton value="Reserve"
26          action="#{reservationBean.reserveSeat}"/>
27      </h:form>
28      <h3>#{reservationBean.result}</h3>
29    </h:body>
30  </html>
```

![](img/009e962758dcc71dbc43a493362e6dc0_1381_0.png)

![](img/009e962758dcc71dbc43a493362e6dc0_1381_1.png)

![](img/009e962758dcc71dbc43a493362e6dc0_1381_2.png)

![](img/009e962758dcc71dbc43a493362e6dc0_1381_3.png)

**Fig. 31.21** | Facelets page that allows a user to select a seat. (Part 2 of 2.)

### ReservationBean.java

类 ReservationBean（图 31.22）定义了在 index.xhtml 页面中使用的 seatType、classType 和 result 属性以及 reserveSeat 方法。当用户在 index.xhtml 中点击 **Reserve** 按钮时，方法 reserveSeat（第 57–74 行）执行。第 61–62 行使用服务端点接口对象（在第 22–23 行创建）调用 Web 服务的 reserve 方法，将选择的座位类型和舱位类型作为参数传递。如果 reserve 返回 true，第 65 行将 result 设置为感谢用户预订的消息；否则，第 67–68 行将 result 设置为通知用户请求的座位类型不可用并指示用户重试的消息。

```java
// Fig. 31.22: ReservationBean.java
// Bean for seat reservation client.
package reservationclient;

import com.deitel.reservation.Reservation;
import com.deitel.reservation.ReservationService;
import javax.faces.bean.ManagedBean;

@ManagedBean( name = "reservationBean" )
public class ReservationBean
{
    // references the service endpoint interface object (i.e., the proxy)
    private Reservation reservationServiceProxy; // reference to proxy
    private String seatType; // type of seat to reserve
    private String classType; // class of seat to reserve
    private String result; // result of reservation attempt

    // no-argument constructor
    public ReservationBean()
    {
        // get service endpoint interface
        ReservationService reservationService = new ReservationService();
        reservationServiceProxy = reservationService.getReservationPort();
    } // end constructor

    // return classType
    public String getClassType()
    {
        return classType;
    } // end method getClassType

    // set classType
    public void setClassType( String classType )
    {
        this.classType = classType;
    } // end method setClassType

    // return seatType
    public String getSeatType()
    {
        return seatType;
    } // end method getSeatType

    // set seatType
    public void setSeatType( String seatType )
    {
        this.seatType = seatType;
    } // end method setSeatType

    // return result
    public String getResult()
    {
        return result;
    } // end method getResult

    // invoke the web service when the user clicks Reserve button
    public void reserveSeat()
    {
        try
        {
            boolean reserved = reservationServiceProxy.reserve(
                getSeatType(), getClassType() );

            if ( reserved )
                result = "Your reservation has been made. Thank you!";
            else
                result = "This type of seat is not available. " +
                "Please modify your request and try again.";
        } // end try
        catch ( Exception e )
        {
            e.printStackTrace();
        } // end catch
    } // end method reserveSeat
 } // end class ReservationBean
```

Fig. 31.22 | Page bean for seat reservation client. (Part 2 of 2.)

## 31.11 Equation Generator: Returning User-Defined Types

我们演示的大多数 Web 服务接收和返回原始类型实例。Web 服务也可以处理类类型的实例。这些类型可以作为参数传递给 Web 服务方法或从 Web 服务方法返回。

本节介绍一个 RESTful EquationGenerator Web 服务，该服务生成类型为 Equation 的随机算术方程。客户端是一个数学辅导应用程序，它接受用户希望尝试的数学题信息（加法、减法或乘法）以及用户的技能水平（1 指定使用 1 到 9 的数字的方程，2 指定涉及 10 到 99 的数字的方程，3 指定包含 100 到 999 的数字的方程）。Web 服务随后生成由适当范围内的随机数字组成的方程。客户端应用程序接收 Equation 并向用户显示示例问题。

### 定义类 Equation

我们在图 31.23 中定义类 Equation。本节中的所有程序都在其相应包中包含该类的副本。除了包名之外，该类在每个项目中都是相同的，因此我们只展示一次。像之前使用的 TextMessage 类一样，服务器-

