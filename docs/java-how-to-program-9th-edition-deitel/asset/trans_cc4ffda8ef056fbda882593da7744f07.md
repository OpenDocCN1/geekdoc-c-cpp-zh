
```
168     if ( board[ location ].equals( MARKS[ PLAYER_X ] ) ||
169         board [ location ].equals( MARKS[ PLAYER_O ] ) )
170         return true; // location is occupied
171     else
172         return false; // location is not occupied
173 } // end method isOccupied
174
175     // place code in this method to determine whether game over
176     public boolean isGameOver()
177     {
178         return false; // this is left as an exercise
179     } // end method isGameOver
180
181     // private inner class Player manages each Player as a runnable
182     private class Player implements Runnable
183     {
184         private Socket connection; // connection to client
185         private Scanner input; // input from client
186         private Formatter output; // output to client
187         private int playerNumber; // tracks which player this is
188         private String mark; // mark for this player
189         private boolean suspended = true; // whether thread is suspended
190
191         // set up Player thread
192         public Player( Socket socket, int number )
193         {
194             playerNumber = number; // store this player's number
195             mark = MARKS[ playerNumber ]; // specify player's mark
196             connection = socket; // store socket for client
197
198             try // obtain streams from Socket
199             {
200                 input = new Scanner( connection.getInputStream() );
201                 output = new Formatter( connection.getOutputStream() );
202             } // end try
203             catch ( IOException ioException )
204             {
205                 ioException.printStackTrace();
206                 System.exit( 1 );
207             } // end catch
208         } // end Player constructor
209
210         // send message that other player moved
211         public void otherPlayerMoved( int location )
212         {
213             output.format( "Opponent moved\n" );
214             output.format( "%d\n", location ); // send location of move
215             output.flush(); // flush output
216         } // end method otherPlayerMoved
217
```
```
218    // control thread's execution
219    public void run()
220    {
221        // send client its mark (X or O), process messages from client
222        try
223        {
224            displayMessage( "Player " + mark + " connected\n" );
225            output.format( "%s\n", mark ); // send player's mark
226            output.flush(); // flush output
227
228            // if player X, wait for another player to arrive
229            if ( playerNumber == PLAYER_X )
230            {
231                output.format( "%s\n%s", "Player X connected",
232                "Waiting for another player\n" );
233                output.flush(); // flush output
234
235            gameLock.lock(); // lock game to wait for second player
236
237            try
238            {
239                while( suspended )
240                {
241                    otherPlayerConnected.await(); // wait for player O
242                } // end while
243            } // end try
244            catch ( InterruptedException exception )
245            {
246                exception.printStackTrace();
247            } // end catch
248            finally
249            {
250                gameLock.unlock(); // unlock game after second player
251            } // end finally
252
253            // send message that other player connected
254            output.format( "Other player connected. Your move.\n" );
255            output.flush(); // flush output
256        } // end if
257        else
258        {
259            output.format( "Player O connected, please wait\n" );
260            output.flush(); // flush output
261        } // end else
262
263        // while game not over
264        while ( !isGameOver() )
265        {
266            int location = 0; // initialize move location
267
268            if ( input.hasNext() )
269                location = input.nextInt(); // get move location
270
```
```
271     // check for valid move
272         if ( validateAndMove( location, playerNumber ) )
273         {
274             displayMessage( "\nlocation: " + location );
275             output.format( "Valid move.\n" ); // notify client
276             output.flush(); // flush output
277         } // end if
278         else // move was invalid
279         {
280             output.format( "Invalid move, try again\n" );
281             output.flush(); // flush output
282         } // end else
283     } // end while
284 } // end try
285 finally
286 {
287     try
288     {
289         connection.close(); // close connection to client
290     } // end try
291     catch ( IOException ioException )
292     {
293         ioException.printStackTrace();
294         System.exit( 1 );
295     } // end catch
296 } // end finally
297 } // end method run
298 
299     // set whether or not thread is suspended
300 public void setSuspended( boolean status )
301 {
302     suspended = status; // set value of suspended
303 } // end method setSuspended
304 } // end class Player
305 } // end class TicTacToeServer

Fig. 27.13 | Server side of client/server Tic-Tac-Toe program. (Part 7 of 7.)

```
1   // Fig. 27.14: TicTacToeServerTest.java
2   // Class that tests Tic-Tac-Toe server.
3   import javax.swing.JFrame;
4
5   public class TicTacToeServerTest
6   {
7       public static void main( String[] args )
8       {
9           TicTacToeServer application = new TicTacToeServer();
10          application.setDefaultCloseOperation( JFrame.EXIT_ON_CLOSE );
11          application.execute();
12      } // end main
13  } // end class TicTacToeServerTest
```

Fig. 27.14 | Class that tests Tic-Tac-Toe server. (Part 1 of 2.)

![](img/009e962758dcc71dbc43a493362e6dc0_1194_0.png)

# Fig. 27.14 | Class that tests Tic-Tac-Toe server. (Part 2 of 2.)

我们首先讨论 Tic-Tac-Toe 游戏的服务器端。当 TicTacToeServer 应用程序执行时，主方法（图 27.14 第 7–12 行）创建一个名为 application 的 TicTacToeServer 对象。构造函数（图 27.13 第 34–69 行）尝试设置一个 ServerSocket。如果成功，程序会显示服务器窗口，然后 main 调用 TicTacToeServer 的 execute 方法（第 72–100 行）。execute 方法循环两次，每次在第 79 行阻塞等待客户端连接。当客户端连接时，第 79 行创建一个新的 Player 对象以作为独立线程管理该连接，第 80 行在 runGame 线程池中执行该 Player。

当 TicTacToeServer 创建一个 Player 时，Player 构造函数（第 192–208 行）接收表示与客户端连接的 Socket 对象并获取相关的输入和输出流。第 201 行通过将 Formatter 包装在套接字的输出流周围来创建一个 Formatter（参见第 17 章）。Player 的 run 方法（第 219–297 行）控制发送到客户端和从客户端接收的信息。首先，它将客户端在进行移动时将在棋盘上放置的字符传递给客户端（第 225 行）。第 226 行调用 Formatter 方法 flush 以强制将此输出发送到客户端。第 241 行在 player X 的线程开始执行时将其挂起，因为 player X 只有在 player O 连接后才能移动。

当 player O 连接时，游戏可以开始，run 方法开始执行其 while 语句（第 264–283 行）。此循环的每次迭代读取一个整数（第 269 行），表示客户端希望放置标记的位置（必要时阻塞等待输入），第 272 行调用 TicTacToeServer 方法 validateAndMove（在第 118–163 行声明）来检查移动。如果移动有效，第 275 行向客户端发送一条相应消息。如果无效，第 280 行发送一条表示移动无效的消息。程序将棋盘位置维护为 0 到 8 的数字（第 1 行 0 到 2，第 2 行 3 到 5，第 3 行 6 到 8）。

validateAndMove 方法（类 TicTacToeServer 中的第 118–163 行）只允许一次一个玩家移动，从而防止他们同时修改游戏的状态信息。如果尝试验证移动的 Player 不是当前玩家（即被允许移动的玩家），它将被置于等待状态，直到轮到它移动。如果正在验证的移动的位置在棋盘上已被占用，

