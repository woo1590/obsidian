```
class CBase         
{
public:   
	CBase(){}
	virtual ~CBase(){}
};

class CDerived : public CBase
{
public:
	void Render();

	CDerived(){}
	~CDerived(){}
};

class CDerived2 : public CBase
{
public:
	void Draw();

	CDerived2(){}
	~CDerived2(){}
}
int main()
{
	CBase* pObj = new CDerived;
	pObj -> Render(); 오버라이딩 되지 않은 함수 실행 불가

	((CDerived*)pObj)->Render(); 실행가능
	((CDerived2*)pObj)->Draw();  실행가능
}

C스타일의 형변환으로도 자식 클래스의 함수를 실행 할 수 있지만 다형성과는 아무런 관련이 없는 위험한 방식이다.
```

**<주의>
상대적으로 안전한 캐스팅만 있을 뿐 캐스팅은 위험요소가 있음

**C++의 캐스팅 연산자
```
static_cast : 컴파일 타임에 캐스팅을 수행(정적 캐스팅), 논리적인 형변환을 해주며 C스타일의 캐스팅과 거의 같지만 좀 더 안전하다.
int iNum = static_cast<int>(3.14f);

장점 : 컴파일 타임에 캐스팅을 수행하기 때문에 동작 속도가 빠름
단점 : 런 타임에 발생하는 보안, 문법적 오류를 확인 할 수 없음


dynamic_cast : 다운 캐스팅을 하기 위한 목적, 다형성을 사용하기 위한 캐스팅, 일반 자료형은 캐스팅불가 
조건
1. 클래스가 상속 관계에 있어야 함.
2. 부모 클래스에 가상 함수가 한 개라도 있어야 함.

장점 : 런 타임시, 비 논리적인 형 변환을 발견하게 되면 nullptr 반환하기 때문에 예외처리를 할 수 있다.
단점 : 캐스팅 속도가 느림. 
class CBase         
{
public:   
	CBase(){}
	virtual ~CBase(){}
};

class CDerived : public CBase
{
public:
	void Render();

	CDerived(){}
	~CDerived(){}
};

int main()
{
	CBase* pDer = new CDerived
	dynamic_cast<CDerived*>(CDerived)->Render();
}
가상 함수가 있어야 하는 이유 : '가상 함수 테이블'을 참조하여 함수를 실행하기 때문에 가상 함수 테이블 생성을 위해 가상 함수가 있어야 함(하다못해 소멸자라도)


const_cast : 포인터나 레퍼런스에 부여된 const 성질을 벗겨내기 위한 도구

int iNum = 10;
const int* p = &iNum;
int *p2 = const_cast<int*>(p);
*p2 = 20;

reinterpret_cast : const 포인터 제외 모든 포인터의 형 변환을 허용
예측 할 수 없는 동작을 할 수 있기 때문에 사용을 권장하지 않는다.

int iNum = 65;
char* ptr = reinterpret_cast<char*>(&iNum);
```

**TMI

RTTI (Run Time Type Information)