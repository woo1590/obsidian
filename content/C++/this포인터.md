
*생성된 객체의 주소 값 - 상수 포인터*

**this포인터의 활용
```
ex) private안에서 객체를 생성하고 소멸시에 this포인터를 사용
class CObj
{
public:
	static CObj* Create()
	{
		CObj* pInstance = new CObj;
		return pInstance;
	}

	void Destroy()
	{
		delete this;
	}
private:
	CObj(){}
	~CObj(){}
};

ex2) 키보드 입력 시 총알을 발사 하는 기능이 있을 때 player 클래스 내부에서 함수를 구현하고 현재 플레이어의 위치를 this포인터를 사용하여 참조

ex3)
```
