# The Concepts of Process and Thread

```
bool bExitApplication;
int iPhilosopherArray[PHILOSOPHER_COUNT];
int PhilosopherCount;
COMMICATIONOBJECT, *pCOMMUNICATIONOBJECT;
```

```
HWORD InitInstance(HINSTANCE hInstance, int nCmddShow)
HATOM MyRegisterClass(HINSTANCE hInstance)
LRESULT CALLBACK WndProc(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
LPARAM (lParam)

int PhilosopherPass(int iPhilosopher)
void FillEllipse(HWND hWnd, HDC hdc, int iLeft, int iTop, int
Right, int iBottom, int iPass);
```

```
TCHAR* szTitle = TEXT("Philosophers Dinner Demo")
TCHAR* szWindowName = TEXT("_PD_WND_CLASS_")
TCHAR* szSemaphoreName = TEXT("_PD_SEMAPHORE_")
nTCHAR* szMappingName = TEXT("_SHARED_FILE_MAPPING_")\nCOMMUNICATIONOBJECT pCommObject = NULL;
```

```
int APIENTRY_wWinMain(HINSTANCE hInstance, HINSTANCE
hPrevInstance, LPFTSTR lpCmdLine, int nCmddShow)
{
   UNREFERENCED_PARAMETER(hPrevInstance);
   UNREFERENCED_PARAMETER(lpCmdLine);

   HANDLE hMapping = CreateFileMapping((HANDLE)-1, NULL,
   PAGE_READWRITE, 0, sizeof(COMMICATIONOBJECT), szMappingName)
   if (!hMapping)
   {
      MessageBox(NULL, TEXT("Cannot open file mapping"),
      TEXT("Error!"), MB_OK);
      return 1;
   }
   pCommObject = (COMMICATIONOBJECT) MapViewOfFile(hMapping,
   FILE_MAP_ALL_ACCESS, 0, 0, 0);
   if (!pCommObject)
   {
      MessageBox(NULL, TEXT("Cannot get access to file mapping!"),\n      TEXT("Error!"), MB_OK);
      CloseHandle(hMapping);
      return 1;
   }
   InitCommonControls();
   MyRegisterClass(hInstance);
HWnd = NULL;
```

68