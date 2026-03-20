`#include <forward_list>`

```cpp
forward_list<int> intFlist;

intFlist.push_front(1);
intFlist.push_front(2);
intFlist.push_front(3);   //push_front로만 원소 추가가 가능

forward_list<int>::iterator iter=intFlist.begin();

iter ++; 가능
iter --; 불가능 (단방향 리스트)
```

**unique()
- 인접한 노드 중에 같은 값을 가진 노드를 삭제

**foward_list와 list
- list에 비해 용량이 적다[^1]
- 앞부분 삽입, 삭제에 대해서는 list보다 빠르다



--------------------------------------------------------------------
[^1]: list는 더블 링크드 리스트, forward_list는 단일리스트
