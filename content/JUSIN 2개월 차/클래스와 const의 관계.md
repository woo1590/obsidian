
**const 멤버 변수
```
class Obj{
private:
	const int iNum;
public:
	Obj(){iNum = 100} 상수이기 때문에 대입을 통한 초기화 불가능
};


clss Obj{
private:
	const int iNum;
public:
	Obj():iNum(100){}  이니셜라이저를 통한 초기화
}

이니셜라이저를 사용하여 상수를 초기화 할 수 있다
대입을 통한 초기화 보다 속도가 더 빠름
```

**const 멤버 함수
```
class Obj{
private:
	const int iNum;
public:
	void Render()const {cout << iNum << endl;} 읽기 전용 함수
};

읽기 전용 함수에서 '멤버 변수'의 쓰기는 불가능하다
멤버 변수가 아닌 다른 변수들의 값 쓰기는 가능하다


멤버 함수 안에서는 읽기 전용 멤버 함수만 호출 할 수 있다. 
class Obj{
private:
	const int iNum;
public:
	void Render()const {cout << iNum << endl;} 읽기 전용 함수
	void Test()const{}
};


생성된 객체의 형식에 따라 함수 오버로딩이 동작한다
class Obj{
private:
	const int iNum;
public:
	void Render()const {cout << iNum << endl;} 읽기 전용 함수
	void Test()const{}
	void Test(){}
};

int main(){
	const Obj O1;    const 함수 호출
	Obj O2;          일반 함수 호출

}

mutable 키워드를 사용하여 읽기 전용 함수 내부에서도 값을 쓸 수 있다
class Obj{
private:
	mutable int iNum;
public:
	void Render()const {
	cout << iNum << endl;
	iNum = 400;              mutable 키워드가 붙은 멤버 변수의 값만 변경 가능
	} 
	
};

```