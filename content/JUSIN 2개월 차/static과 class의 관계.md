
**static 변수 (class 변수)
```
class OBJ
{
private:
	static int m_iA;  static변수는 멤버 변수가 아님
public:
	OBJ(){}
	void Render() { cout << m_iA << endl; }
};


멤버 변수 : class의 구성 멤버

클래스 변수 : 객체의 멤버가 아니다. 다만 OBJ의 네임스페이스를 통해 접근 가능

int OBJ:: m_iA = 100; 클래스 변수 초기화(외부 기호이기 떄문에 클래스 외부에서 초기화를 시켜야 한다.)
```


**static 함수(class 함수)
```
class OBJ
{
private:
	int m_iA=100;
public:
	static void Render()
	{
		m_iA = 99;        멤버 변수 읽기/쓰기 불가
		cout<<m_iA<<endl;
	}
};


class함수는 객체 생성 이전에도 사용할 수 있기 때문에 함수 내부에서 멤버 변수 사용이 불가능하다.
```


클래스의 양이 적은 소규모 프로젝트에서는 잘 사용하지 않지만
큰 프로젝트에서는 static이 유용하게 사용된다.

주로 *클래스 사이에서 전역적으로 사용되는  상호작용*(충돌처리) 기능들을 static함수와 변수로 만들어 클래스에 담아 관리한다