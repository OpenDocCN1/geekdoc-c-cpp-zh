

```matlab
% stop. All inputs are passed to gui1_OpeningFcn via varargin.
%
```

### 初始化代码

```matlab
gui_Singleton = 1;
gui_State = struct('gui_Name', mfilename, ...
    'gui_Singleton', gui_Singleton, ...
    'gui_OpeningFcn', @gui1_OpeningFcn, ...
    'gui_OutputFcn', @gui1_OutputFcn, ...
    'gui_LayoutFcn', [], ...
    'gui_Callback', []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end

if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end
% End of Initialization code

% --- Executes just before gui1 is made visible.
function gui1_OpeningFcn(hObject, eventdata, handles, varargin)
% This function has no output args, see OutputFcn.
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
x = get(handles.slider1,'Value')
set(handles.text1,'String',num2str(x))

% --- Executes during object creation, after setting all properties.
function slider1_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background, change
%       'usewhitebg' to 0 to use default.
usewhitebg = 1;
if usewhitebg
    set(hObject,'BackgroundColor',[.9 .9 .9]);
else
    set(hObject,'BackgroundColor',get(0, 'defaultUicontrolBackgroundColor'));
end

% --- Executes during object creation, after setting all properties.
function slider2_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background, change
%       'usewhitebg' to 0 to use default.
usewhitebg = 1;
if usewhitebg
    set(hObject,'BackgroundColor',[.9 .9 .9]);
else
    set(hObject,'BackgroundColor',get(0, 'defaultUicontrolBackgroundColor'));
end

% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
p = get(handles.slider1,'Value');
q = get(handles.slider2,'Value');

a = newfis('wash_machine1');
a = addvar(a,'input','x',[0 100]);
a = addmf(a,'input',1,'A1','trimf',[0 0 50]);
a = addmf(a,'input',1,'A2','trimf',[0 50 100]);
a = addmf(a,'input',1,'A3','trimf',[50 100 100]);

a = addvar(a,'input','y',[0 100]);
a = addmf(a,'input',2,'B1','trimf',[0 0 50]);
a = addmf(a,'input',2,'B2','trimf',[0 50 100]);
a = addmf(a,'input',2,'B3','trimf',[50 100 100]);

a = addvar(a,'output','z',[0 60]);
a = addmf(a,'output',1,'C1','trimf',[0 8 12]);
a = addmf(a,'output',1,'C2','trimf',[8 12 20]);
a = addmf(a,'output',1,'C3','trimf',[12 20 30]);
a = addmf(a,'output',1,'C4','trimf',[30 40 50]);
a = addmf(a,'output',1,'C5','trimf',[50 60 70]);

rulelist = [ ...
    1 1 1 1 1
    2 2 3 1 1
    3 3 5 1 1
    1 2 3 1 1
    1 3 3 1 1
    2 1 2 1 1
    2 3 4 1 1
    3 1 2 1 1
    3 2 4 1 1];

a = addrule(a, rulelist);

z = evalfis([p q], a)

set(handles.text3,'String',num2str(z))
set(handles.slider4,'Value',z)

% --- Executes on slider movement.
function slider3_Callback(hObject, eventdata, handles)
% hObject    handle to slider3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider

% --- Executes during object creation, after setting all properties.
function slider3_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background, change
%       'usewhitebg' to 0 to use default.
usewhitebg = 1;
if usewhitebg
    set(hObject,'BackgroundColor',[.9 .9 .9]);
else
    set(hObject,'BackgroundColor',get(0, 'defaultUicontrolBackgroundColor'));
end

% --- Executes on slider movement.
function slider4_Callback(hObject, eventdata, handles)
% hObject    handle to slider4 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider

% --- Executes during object creation, after setting all properties.
function slider4_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider4 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background, change
%       'usewhitebg' to 0 to use default.
usewhitebg = 1;
if usewhitebg
    set(hObject,'BackgroundColor',[.9 .9 .9]);
else
    set(hObject,'BackgroundColor',get(0, 'defaultUicontrolBackgroundColor'));
end
```

### 输出

图 8.2 和图 8.3 分别展示了当污垢程度为 70.2041% 和 22.449% 时模糊洗衣机的图形用户界面。

### 仿真结果

输入变量“x”和“y”分别表示污垢类型和污垢百分比。输出变量“z”表示洗衣机去除污垢所需的时间。部分观测结果列于表 8.1。

因此，以上部分讨论了带有 GUI 的模糊洗衣机的运行情况，以及在 MATLAB 中设计的模糊控制器，并给出了一些结论性观察。

**表 8.1：** 模糊洗衣机的观测结果

| 序号 | 污垢类型“x” | 污垢百分比“y” | 洗涤时间“z” |
|---:|---:|---:|---:|
| 1 | 72.58 | 39.59 | 29.07 |
| 2 | 14.92 | 03.67 | 10.39 |
| 3 | 12.50 | 40.00 | 17.63 |
| 4 | 26.62 | 73.06 | 30.43 |
| 5 | 85.46 | 87.35 | 40.27 |
| 6 | 96.37 | 97.55 | 49.63 |

![当污垢程度为 70.2041% 时模糊洗衣机的 GUI](img/d9a4cc12c48f7466f309cbd3c4549c73_343_0.png)

**图 8.2：** 当污垢程度为 70.2041% 时模糊洗衣机的 GUI

![当污垢程度为 22.449% 时模糊洗衣机的 GUI](img/d9a4cc12c48f7466f309cbd3c4549c73_343_1.png)

**图 8.3：** 当污垢程度为 22.449% 时模糊洗衣机的 GUI

## 8.2 示例 2 - 油轮模糊控制系统

该程序模拟油轮的模糊控制系统。它有一个模糊控制器，具有两个输入：船舶航向误差（e）和该误差的变化（c）。模糊控制器的输出是舵输入（delta）。我们希望油轮航向（psi）跟踪参考输入航向（psi_r）。我们将油轮模拟为一个连续时间系统，该系统由在数字计算机上实现的模糊控制器控制，采样间隔为 T。

该程序可用于说明：

- i) 为模糊控制器编写代码（针对两个输入和一个输出，说明一些简化计算的方法，针对三角形隶属函数，以及重心法或中心平均法去模糊化）。
- ii) 调节模糊控制器的输入和输出增益。
- iii) 被控对象条件变化（“压载”和“满载”）的影响。
- iv) 传感器噪声（航向传感器噪声）、对象扰动（风吹击船侧）和对象运行条件（船速）如何影响性能。
- v) 缩放增益选择不当如何导致振荡（极限环）。
- vi) 缩放增益（或规则库）选择不当如何导致系统不稳定。
- vii) 通过绘制模糊控制器的输入-输出映射，展示由模糊控制器实现的非线性形状。

### MATLAB 代码

```matlab
clear  % Clear all variables in memory
% Initialize ship parameters
% (Can test two conditions, "ballast" or "full"):

ell = 350;    % Length of the ship (in meters)
```

