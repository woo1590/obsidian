
*string 헤더파일을 포함해야 사용 가능*
```
#include <string>    stl에서 제공하는 문자열 기반 클래스 템플릿


tmi
#include <string.h>   c언어 시절부터 존재
#include <cstring>    mfc에서 제공하는 문자열 클래스 헤더 파일
```

**char 배열과 string의 차이점

```
char Name[32] = "hello"
char Temp[32] = {};

Temp = Name    불가능
strcpy_s() 함수를 사용해야 한다



string Name = "hello";
string Temp = Name;    대입 가능


string Name = "hello";
string Temp = "world";

Temp += Name        "helloworld"   + 연산자 사용 가능


char Name[32] = "hello";
string Temp = "";

Temp = Name;     연산 가능

더 편리하게 문자열을 다룰 수 있음
```

**char 와 string의 호환
```
char Name[32] = "hello";
string Temp = "";

strcpy_s(Name, sizeof(Name), Temp.c_str())

c.str() 함수를 사용해야 호환 가능
```
