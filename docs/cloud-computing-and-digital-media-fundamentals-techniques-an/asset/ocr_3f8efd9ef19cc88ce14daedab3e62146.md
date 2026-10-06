# 240 Cloud Computing and Digital Media

![](bbox=[0.137, 0.085, 0.862, 0.423])

FIGURE 10.1 The layout of a game record editor.

(SGF) 8). In addition to storing and querying, some game record editors also support the extensive features such as variations in move tree, move comments, threat hints, and plug-ins.

We modified the open-source editor named RenLib to fit our applications such as Connect6 [5], Go, and Chinese Chess. Figure 10.1 shows the layout of our game record editor. The panel in the lower left part of the figure is the board view that shows the current position. The one in the lower right part is the tab window that provides the users with some utilities, for example comments on a position or a console output for debugging. Toolbars on the top are used to provide the users with a variety of functionalities via buttons.

The game editing mode uses the model-view-controller (MVC) design pattern and includes two components: model and view corresponding to the same name in MVC. The controller is not encapsulated into a class because we use Microsoft foundation classes (MFC) to construct our software framework that has its own mechanism to map user interface (UI) events to functions.

The JL module accepts the game tree search jobs from the game record editor and dispatches them to the workers for running. The jobs include by giving a start position, finding the best move, expanding all moves, or