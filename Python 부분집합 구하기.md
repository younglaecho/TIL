# Python 부분집합 구하기

파이썬에서 부분집합을 구하는 방법은 여러가지가 있겠지만, 그 중에서 두가지만 소개하겠다.
첫 번째 방법은 python의 내장 라이브러리인 itertools를 이용한 방법이고, 두 번째 방법은 비트연산을 이용한 방법이다.

## itertools를 활용하여 부분집합 구하기

```python
from itertools import combinations

a = [1, 2, 4]
result = []
result2 = []
for i in range(0, len(a)+1):
    c = combinations(a, i)
    result.extend(c)

print(result)
# [(), (1,), (2,), (4,), (1, 2), (1, 4), (2, 4), (1, 2, 4)]
```

itertools의 combination이라는 함수의 첫번째 매개변수로 부분집합을 구할 대상을 넣고, 두번째 매개변수로 부분집합의 원소를 입력한다.
위의 예시와 같이 반복문을 사용하여 부분집합 전체를 구할 수 있다.



## 비트연산을 활용하여 부분집합 구하기

```python
arr = [1, 2, 3]
n = len(arr)
result = []
for i in range(1 << n): # 1<<n : 원소의 개수만큼의 길이를 가진 
    string = ''
    for j in range(n): 
        if i & (1 << j):	 # 1<<j : 001 , 010, 100 
          								 # if i & (1 << j) : 각각의 i 별로 j와 겹치는 영역이 있는지 확인
            string += str(arr[j])
    result.append(string)

print(result)

```

비트연산을 활용하여 각각의 자리수를 모두 순회하면서 부분집합을 구하는 방법이다. 각각의 자리를 모두 순회하기 때문에 나올 수 있는 모든 조합을 구할 수 있다.

