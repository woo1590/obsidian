
`sort(begin, end, 조건자)`

```cpp
vector<int> vecInt;

vecInt.push_back(1);
vecInt.push_back(4);
vecInt.push_back(3);
vecInt.push_back(5);
vecInt.push_back(2);

//오름차순 정렬
sort(vecInt.begin(), vecInt.end());

//조건자
bool Less(int iDst, int iSrc)   //함수 포인터 형식
{
	return iDst<iSrc;
}

struct Less      //함수 객체 형식
{
	template<typename T>
	bool operator()(T Dst, T Src)
	{
		return Dst<Src;
	}
}
//람다식도 가능
//functional 헤더에서 제공하는 조건자 사용가능. less, greater . . . 
```
- 퀵 정렬을 기반으로 만들어진 정렬 알고리즘[^1]
- 배열 기반 컨테이너에만 사용 가능(vector, deque ...)

--------------------------------------------------------------------

`count_if`
- 컨테이너 원소를 순회하며 매개 변수로 전달한 조건자에 따라 참에 해당하는 원소 개수 반환
- 반환 값은 size_t

```cpp
bool OddNum(int iNum)
{
	return iNum%2;
}

vector<int> vecInt;

vecInt.push_back(1);
vecInt.push_back(4);
vecInt.push_back(3);
vecInt.push_back(5);
vecInt.push_back(2);

size_t iCount=count_if(vecInt.begin(), vecIng.end(),OddNum)
```

--------------------------------------------------------------------

`for_each`
- for문과 같음, 조건자에 의해 반복의 수행 여부를 결정

```cpp
template<typename T>
void Safe_Del(T& p)
{
	delete p;
	p = nullptr;
}

vector<int*> vecInt;
.
.
.
.
.

for_each(vecIntp.begin(), vecIntp.end(), Safe_Del<int*>);
vecIntp.clear();
```

`find_if`
- 특정 조건자와 일치하는 원소를 찾는 알고리즘
- 찾고자 하는 원소를 가리키는 반복자 반환
- 찾는 원소가 없는 경우에는 end를 반환

```cpp
bool FindData(const char* pData)
{
	return !strcmp(pData,"b");
}

vector<const char*> vecChar;

vecChar.push_back("a");
vecChar.push_back("b");
vecChar.push_back("c");

vector<const char*>::iterator iter=find_if(vecChar.begin(), vecChar.end(), FindData)
```


**함수 포인터 조건자의 한계
- 매개변수를 전달 할 수 없기 때문에 조건자 내부로 값을 전달 할 수 없음
- 함수 객체 사용시 생성자를 통해 외부 데이터를 가져올 수 있음(우회)
- 람다식 사용시에는 더 유연하게 사용가능

--------------------------------------------------------------------
[^1]: 원소의 개수에 따라 다른 방식의 정렬이 사용됨. sort!=퀵 정렬
