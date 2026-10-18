
## 6.2.8 User Interface

In the previous sections, we saw the evolution of the *CurrencyExchange* project: its two versions, both encompassed in the hierarchical namespaces `CurrExchanger` and its nested `OnLine_CurrExchanger`. `CurrExchanger` defines very basic functionality, whereas `OnLine_CurrExchanger` extends the functionality to automatically load currency information from the Internet. Both were tested as standalone terminal applications. We also saw how to split the project into a static library named *CurrencyCalc_Lib* and another component, *CurrencyCalc_Terminal*, which builds a terminal window application (Section 6.2.6). Now it is time to take the next step and to add a graphical user interface (GUI) to this project. Hence, we will create a third software component to launch *CurrencyExchanger* as a GUI application: `CurrencyCalc_GUI`. The UML component diagram in Figure 6.8 will now change as shown in Figure 6.9.

In this section, we are mostly interested in the `CurrencyCalc_GUI` component, which will be able to draw graphical widgets, as well as process system events, as will be shown. However, the GUI components depend heavily on the type of OS we are working in. This means if we tried to write our `CurrencyCalc_GUI` for two or three different OSs, we would need to write two or three quite different versions of the component. On the other hand, even if our task was much simpler and only one OS was our target, using the raw API would not be the most productive option. A much better solution is to use one of the GUI libraries that create a type of interface between a user application like *CurrencyCalc* and one or many different OSs. Appendix A.4 contains a brief overview of the GUI libraries for C++ projects. Alas, every rose has its thorns, and each has its own peculiarities and limitations. In our example, we chose to test the FLTK library mostly because it is free, it is written entirely in C++, and it runs on many OSs.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_430_0.png)

**Figure 6.9** UML component diagram of the various software components used in our *CurrencyCalc* project. Because the currency exchange engine is extracted into a separate library, we can easily construct a terminal window or GUI application without interference.

[PAGE 431]

So, let’s take a closer look at the UML component diagram shown in Figure 6.9. The most important change is that we have separated all the components strictly related to currency exchange from user-related input-output operations. Now these components are enclosed in a separate library, whereas user actions are moved to different application projects. As a result, we achieve the following important goals:

- **Code readability** – It is now much easier to concentrate on various levels of our system. That is, when working on further mechanisms for currency exchange, we will touch only the *CurrencyCalc_Lib* library. When working on user interfaces, we will not need to change anything in the currency exchange library.
- **Code reusability** – It is much easier to reuse our *CurrencyCalc_Lib* library in any other project (with or without a user interface) that requires currency exchange actions. It is also much easier to extend the functionality of the library.

Hence, a rule of thumb is not to get involved with the cout and cin objects in classes. Input/output operations should be implemented using the external overloaded operator << and operator >>.

Our code will finally display graphics. To do so, we need to install the FLTK library. Details of this operation are described on the FLTK web page (FLTK 2019) and depend on our OS and installed tools. However, the following short guide can be useful:

- 1. Download FLTK from its website and unpack it with the *FLTK* and *CurrencyCalc* directories at the same level.
- 2. Go into the *FLTK* directory, and launch `cmake .` [dot] to build the FLTK project in the current directory.
- 3. Open the project, and build the library. When finished, the *FLTK/Lib/Debug* directory should contain the *fltkd.lib* library (verify its build date and time).

# 6.2.8.1 Definition of the CC_GUI Class

Listing 6.8 shows the definition of the CC_GUI class that defines a user interface for our *CurrencyCalc* application, and Listing 6.9 contains its full implementation. We will briefly explain what these do.

As usual, at the beginning of a new definition, we should inform the compiler about the classes we wish to use. In this example, this is done in two forms. First, on lines [1–5], the header files are included, which contain the definitions of some SL containers as well as the definitions of the XML_CurrencyExchanger and functions defined in the *CurrencyCalcPlayGround* header. As a result, all classes defined in this unit will know about XML_CurrencyExchanger but not vice versa, as shown by the arrows in Figure 6.9. Lines [8–12] contain the forward declarations. This is the second way to introduce externally defined classes into the scope of the current translation unit. But in this case only pointers and references to these external classes can be used, since their definitions are not provided. Then, on line [14], a namespace shortcut OL_CE is introduced, to increase readability and save on typing.

The definition of the CC_GUI class starts on line [18]. Thanks to the aforementioned forward declarations, on lines [23–26] we can define pointers to components (widgets) of the GUI. After initialization, these will point at the real widget objects. Although using pointers is not the preferable indirect access technique in modern C++, it is the only option in legacy code like the FLTK library. In many real situations, we face the problem of connecting the two worlds; what is important is to do so safely.

[PAGE 432]

<!-- no content -->

[PAGE 433]

# Listing 6.8 (continued)

```
```cpp
Fl_Value_Output *        fStaticEditWidget {};
Fl_Window *              fMainWindow {};

private:

// An interface to our currency calculator component
using XCE = OL_CE::XML_CurrencyExchanger;

XCE &    fXML_CurrencyExchanger;

// Initial code of the reference currency
std::wstring    fFromCurrencyCode;

public:

CC_GUI( XCE & xce, const std::wstring & fromCurrency = L"PLN" );

virtual ~CC_GUI();

private:

////////////////////////////////////////////////////////////
// CALLBACK FUNCTION -- do NOT modify !!!
////////////////////////////////////////////////////////////
//
// INPUT:
//       widgetPtr - a pointer to the button widget
//       obj - a pointer "this" to CC_GUI object
//
// OUTPUT:
//       none
//
// REMARKS:
//       A static function to be put as the FLTK button callback
//       Delegates an action to the Action_On_Button().
//
static void theButtonCallback( Fl_Widget * widgetPtr, void * obj );

protected:

////////////////////////////////////////////////////////////
// Local function to process button requests
////////////////////////////////////////////////////////////
//
// INPUT:
//       none
//
// OUTPUT:
//       true if ok
//
// REMARKS:
//
virtual bool Action_On_Button( void );

private:

////////////////////////////////////////////////////////////
// Converter of a three-letter code to one word with bytes
// set with code characters.
////////////////////////////////////////////////////////////
//
```
```

[PAGE 434]

<!-- no content -->

[PAGE 435]

# **Listing 6.9**  Implementation of the `CC_GUI` class (in *CurrencyCalc_GUI, CurCalc_GUI.cpp*).

```
```cpp
// #include group here (FLTK & SL)

// using declarations
using std::string;
using std::wstring;
using std::vector;

#include "CurCalc_GUI.h"
#include "StringConverters.h"

// Class parametric constructor
CC_GUI::CC_GUI( XCE & xce, const wstring & fromCurrency /*= L"PLN"*/ )
    : FXML_CurrencyExchanger( xce ),
      fromCurrencyCode( fromCurrency )
{
}

// Destructor does nothing - in case of derivation it is defined virtual
CC_GUI::~CC_GUI()
{
}
```
```

Lines [13–15] define the class constructor, and line [20] is reserved for the class virtual destructor, for the reasons we have discussed.

Let’s take a closer look at the `theButtonCallback` static function whose definition starts on line [24]. As already mentioned, this is a function that will be registered to the FLTK framework to be called in response to the event of a button click by the user. It accepts two parameters: `widgetPtr`, which will point at the widget object from FLTK; and `obj`, which conveys whatever parameter we pass when registering the `theButtonCallback` to the FLTK callback mechanism. And here is a trick: for the future `obj`, we will pass a pointer this to the `CC_GUI` object. This way, a *double dispatch mechanism* will be achieved, as illustrated in Figure 6.10.

Such a communication mechanism based on passing a function through its pointer may be encountered in older legacy code such as FLTK. Other platforms rely on similar ideas of signals and/or message passing, but embedded in the object-oriented framework (Appendix A.4).

Programmatically, to perform the previously described action, the passed `obj` pointer needs to be cast to the `CC_GUI` pointer type. This is achieved on line [27] with the `reinterpret_cast` operator, described in Table 3.15 (*GROUP 2*). Then, the call to the virtual `Action_On_Button` occurs on line [30].

```
```cpp
// CALLBACK FUNCTION - do NOT modify !!!
void CC_GUI::theButtonCallback( Fl_Widget * widgetPtr, void * obj )
{
    // Convert the input pointer to our class object
    CC_GUI * theObj = reinterpret_cast< CC_GUI * >( obj );

    // Call button handler function
    theObj -> Action_On_Button();
}
```
```

The `Action_On_Button` function, defined on line [35], performs the action associated with currency exchange computations. Since an exception can happen here, the code is encompassed
