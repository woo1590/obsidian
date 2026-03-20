캡슐화

캡슐화는 **데이터(멤버 변수)** 와 **그 데이터를 다루는 기능(멤버 함수)** 을 하나의 클래스 안에 묶는 개념이다.  
  
즉, 클래스의 멤버 변수를 변경하거나 출력하는 함수들을 모두 **클래스 내부의 멤버 함수**로 작성하는 방식이다.

은닉화

```cpp
class Test {
private:
	int m_iX;
	int m_iY;
public:
	void Render();
	void SetX_Y(int _iX, int _iY);
};

멤버 함수를 통해서 멤버 변수에 접근해야 한다

void Test::Render()
{
	cout << m_iX << endl;
	cout << m_iY << endl;
}

void Test::SetX_Y(int _iX, int _iY)
{
	m_iX = _iX;
	m_iY = _iY;
}

Access Method : 멤버 변수에 접근하기 위한 함수들
ex) Get, Set 함수들
```

**접근제어 지시자
- public : 내부, 외부 모드 접근 가능
- protected : 자식 클래스에서만 접근 가능
- private : 내부만 접근 가능( 같은 { } )

*class의 멤버 변수들은 private으로 사용*
*class의 멤버 함수들은 public으로 사용*

상속성
```cpp
class CObj
{
public:
	CObj(){}
	~CObj(){}
protected:
};

class CPlayer:public CObj
{
public:
	CPlayer() {}
	~CPlayer() {}
private:
};

int main()
{
	CPlayer Player;
	return 0;
}
```

*파생 클래스 선언시에는 기반 클래스의 헤더파일을 포함해야 한다.*

**자식 객체 생성과정
1. 메모리 할당
2. 부모 생성자 호출
3. 자식 생성자 호출

**자식 객체 소멸 과정
1. 자식 소멸자 호출
2. 부모 소멸자 호출
3. 메모리 반환

```cpp
class CObj
{
public:
	CObj(){}
	~CObj(){}
protected:
	int m_iA;
};

class CPlayer:public CObj
{
public:
	CPlayer() {}
	~CPlayer() {}
private:
	int m_iA;
};

만약 부모와 자식 클래스에 같은 이름의 변수가 있다면 ::을 통해 접근하거나 this포인터를 통해 판단한다
```

**is-a 관계
- 자식 클래스로 갈 수록 특성이 구체화 됨
- 사람-남자(남자는 사람이다)

**has-a 관계
- 플레이어가 가지는 무기, 방어구 등등 소유 관계는 아니지만 종속성이 있는것들


**객체 포인터 권한
```cpp
class CObj
{
public:
	void Render();
};


class CPlayer:public CObj
{
public:
	void Render_Player();
};

int main()
{
	CObj* pPlayer = new CPlayer;

	pPlayer->Render(); 가능
	pPlayer->Render_Player(); 불가능

생성한 객체는 CPlayer이지만 포인터의 타입이 CObj이기 때문에 CPlayer에 어떤 함수가 있는지 알 수 없음
}

정적 바인딩: 컴파일 타임에 이미 어떤 함수를 호출 할 지 그 권한이 결정 되어 있는 상태
```


상속의 이점
- 공통으로 포함 된 함수들로 여러가지 객체들을 쉽게 관리할 수 있다

다형성

**[[오버라이딩]]

**[[다운 캐스팅(dynamic cast)]]

**<정리>

공통적인 기능이지만 세부적인 디테일이 다를 때는 오버라이딩,
하나의 파생 클래스에서만 가지고 있는 기능은 다운 캐스팅을 하는것이 다형성에 알맞은 방식

