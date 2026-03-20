### API란?
- Appilcation 
- 앱을 개발하기 위한 도구

### Win32API
- C언어 기반의 API

### MFC
- C++ 기반의 API
- 최근에는 거~의 사용하지 않음


-----
### 인스턴스

### 핸들
- 운영체제가 리소스를 관리하기 위해 부여하는 일종의 번호(16진수 정수)

----
### Win32API 기본 

**MyRegisterClass
```cpp
ATOM MyRegisterClass(HINSTANCE hInstance)
{
    WNDCLASSEXW wcex;   
    // 윈도우 창 생성을 위해 값을 채워야할 구조체

    wcex.cbSize = sizeof(WNDCLASSEX);       
    // 자기 자신의 사이즈를 저장

    wcex.style          = CS_HREDRAW | CS_VREDRAW;

    // 가로 다시 그리기 | 세로 다시 그리기
    // 윈도우 창의 스타일 정의, 초기화 되는 값이 창의 수평, 수직 크기가 변할 경우 다시 그리기를 말하는 옵션

    wcex.lpfnWndProc    = WndProc;
    // 메세지 처리기 함수의 이름을 전달

    wcex.cbClsExtra     = 0;
    wcex.cbWndExtra     = 0;
    // 윈도우가 특수한 목적으로 사용하는 여분의 공간(일종의 예약 영역)

    wcex.hInstance      = hInstance;
    // 윈도우 클래스를 사용하는 프로그램의 번호를 설정, main함수 매개 변수 전달 값이 자동 사용

    wcex.hIcon          = LoadIcon(hInstance, MAKEINTRESOURCE(IDI_DEFAULTWINDOW));
    // 윈도우 차이 사용할 아이콘 지정

    wcex.hCursor        = LoadCursor(nullptr, IDC_ARROW);
    // 창에서 사용할 마우스 커서

    wcex.hbrBackground  = (HBRUSH)(COLOR_WINDOW+1);
    // 창 배경 색상

    wcex.lpszMenuName = NULL; //MAKEINTRESOURCEW(IDC_DEFAULTWINDOW);
    // 창 메뉴

    wcex.lpszClassName  = szWindowClass;
    // 실행 파일 이름 지정

    wcex.hIconSm        = LoadIcon(wcex.hInstance, MAKEINTRESOURCE(IDI_SMALL));
    // 창 상단의 아이콘

    return RegisterClassExW(&wcex);
}

```

**InitInstance
```cpp
BOOL InitInstance(HINSTANCE hInstance, int nCmdShow)
{
   hInst = hInstance; // 인스턴스 핸들을 전역 변수에 저장합니다.

   HWND hWnd = CreateWindowW(szWindowClass,     // 클래스 이름(실행 파일 이름)
                            szTitle,            // 창 위에 띄울 문자열
                            WS_OVERLAPPEDWINDOW, 
                            // 윈도우 스타일 옵션(기본 창 모양)
                            CW_USEDEFAULT, 0,   // 창 생성 위치(X, Y 좌표)
                            800, 600,           // 창의 가로, 세로 사이즈
                            nullptr,            // 부모 윈도우 핸들
                            nullptr,            // 윈도우에서 사용할 메뉴 핸들
                            hInstance,          // 윈도우를 만드는 주체
                            nullptr);           // 운영체제가 특수한 목적으로 사용

   if (!hWnd)
   {
      return FALSE;
   }

   ShowWindow(hWnd, nCmdShow);
   UpdateWindow(hWnd);

   return TRUE;
}
```

**WndProc(중요)
```cpp
LRESULT CALLBACK WndProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam)
{
    switch (message)
    {
    case WM_CREATE:

        SetTimer(hWnd, 0, 0, 0);
        
        // 타이머 설치 함수
        // 1. 윈도우 핸들
        // 2. 타이머 id
        // 3. 타이머 주기(default 1 / 1000)
        // 4. NULL인 경우 3 매개 변수 주기로 WM_TIMER 메세지를 발생시킴
        break;

    case WM_TIMER:

        InvalidateRect(hWnd, 0, TRUE);

        // 윈도우 갱신 함수
        // 1. 갱신할 윈도우 핸들
        // 2. 윈도우 갱신 범위(NULL 인 경우 화면 전체 영역)
        // 3. TRUE : 그려져 있지 않는 부분도 갱신
        //   FALSE : 새로 그리는 부분만 갱신
        break;

    case WM_COMMAND:
        {
            int wmId = LOWORD(wParam);
            // 메뉴 선택을 구문 분석합니다:
            switch (wmId)
            {
            case IDM_ABOUT:
                DialogBox(hInst, MAKEINTRESOURCE(IDD_ABOUTBOX), hWnd, About);
                break;
            case IDM_EXIT:
                DestroyWindow(hWnd);
                break;
            default:
                return DefWindowProc(hWnd, message, wParam, lParam);
            }
        }
        break;
    case WM_PAINT:
        {
            PAINTSTRUCT ps;
            // dc : 출력에 관한 정보를 갖고 있는 구조체
            HDC hdc = BeginPaint(hWnd, &ps);
            EndPaint(hWnd, &ps);
        }
        break;
    case WM_DESTROY:
        PostQuitMessage(0);
        break;
    default:
        return DefWindowProc(hWnd, message, wParam, lParam);
    }
    return 0;
}
```