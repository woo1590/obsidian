
*멤버변수에 접근 할 수 있게 해주는 키워드*
```
class CBoy
{
public:
	CBoy(int _iNum):m_iA(_iNum){}

	friend void CGirl::Draw();     CGirl클래스의 Draw 함수만 CBoy 멤버 변수 접근 가능
	friend class CGril;            CGirl클래스 전체에서 CBoy 멤버 변수 접근 가능
private:
	int m_iA;
}

class CGirl
{
public:
	void Draw()
	{
		CBoy Temp(100);
		Temp.m_iA = 200;
		cout << m_iA << endl;
	}
}
```