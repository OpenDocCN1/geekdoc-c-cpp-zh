```
```matlab
% stop. All inputs are passed to gui1OpeningFcn via
varargin.
%
%```
```

# Initialization code

```
```matlab
gui_Singleton = 1;
gui_State = struct('gui_Name', mfilename, ...
    'gui_Singleton', gui_Singleton, ...
    'gui_OpeningFcn', @gui1_OpeningFcn, ...
    'gui_OutputFcn', @gui1_OutputFcn, ...
    'gui_LayoutFcn', [ ], ...
    'gui_Callback', [ ] );
if nargin & ischar(varargin{1})
gui_State.gui_Callback = str2func(varargin{1});
end
if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State,
    varargin{:});
else
gui_mainfcn(gui_State, varargin{:});
end
```
```

```
```matlab
% End of Initialization code
```
```

```
```matlab
% --- Executes just before gui1 is made visible
```
```

```
```matlab
function gui1_OpeningFcn(hObject, eventdata,
handles, varargin)
% This function has no output args, see OutputFcn.
% hObject handle to figure
% eventdata reserved - to be defined in a future
version of MATLAB
% handles structure with handles and user data (see
GUIDATA)
```
```