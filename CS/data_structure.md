## 목차

- [자료구조란 무엇인가요](#자료구조란-무엇인가요)

  - 효율적으로 데이터를 관리해야 하는 이유 (예)

- [대표적인 자료구조는 어떤 것들이 있나요](#대표적인-자료구조는-어떤-것들이-있나요)

  - 선형 구조
  - 비 선형 구조

- [리스트](#리스트)
- [큐](#큐)
- [스택](#스택)
- [링크드 리스트](#링크드-리스트)
- [해쉬 테이블](#해쉬-테이블)
- [트리](#트리)
- [힙](#힙)
- [그래프](#그래프)

### 자료구조란 무엇인가요

자료구조란 대량의 데이터를 효율적으로 관리할 수 있는 데이터의 구조를 의미합니다

코드 상에서 효율적으로 데이터를 처리하기 위해, 데이터 특성에 따라, 체계적으로 데이터를 구조화해야 합니다

어떤 데이터 구조를 사용하느냐에 따라, 코드의 효율이 달라질 수 있습니다

<br/>

#### 효율적으로 데이터를 관리해야 하는 이유 (예)

우편번호: 5자리 우편번호로 국가의 기초구역을 제공

5자리 우편번호에서 앞 3자리는 시, 군, 자치구를 표기, 뒤 2자리는 일련번호로 구성

학생 관리: 학년, 반, 번호를 학생에게 부여해서, 학생부를 관리

XX학년, X반, X번 학생

만약 위 관리 기법이 없다면, 3000명 학생 중 특정 학생을 찾기 위해, 전체 학생부를 모두 훑어야 함

<br/>

### 대표적인 자료구조는 어떤 것들이 있나요

|              자료구조               |       자료구조        |
| :---------------------------------: | :-------------------: |
|              선형 구조              |      비선형 구조      |
| 리스트 <br/> 스택 <br/> 큐 <br/> 덱 | 트리<br/> 그래프<br/> |

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F2747733A57E8CD8D061E92" alt="자료구조">

출처: https://boycoding.tistory.com/32

<br/>

#### 선형 구조란 무엇인가요

**선형 구조 (Linear Structure)**

> 데이터들이 일렬로 쭉 저장되어 있는 형태

#### 비 선형 구조란 무엇인가요

**비 선형 구조 (Non-Linear Structure)**

> 데이터가 트리 형태로 저장되어 있다고 생각하고 사용하는 자료구조

<br/>

### 리스트

- 데이터를 나열하고, 각 데이터를 인덱스에 대응하도록 구성한 데이터 구조
- 파이썬에서는 리스트 타입이 배열 기능을 제공함

`리스트는 왜 필요한가요?`

- 같은 종류의 데이터를 효율적으로 관리하기 위해
- 같은 종류의 데이터를 순차적으로 저장하기 위해

`장점`

- 빠른 접근이 가능하다
- 첫 데이터의 위치 `[0]`에서 상대적인 위치로 데이터에 접근이 가능하다 (인덱스 번호로 접근이 가능하다)

`단점`

- 데이터 추가/ 삭제가 어렵다
- 미리 최대 길이를 지정해야 함

`make a list using C`

- C 언어에서 배열을 사용할 경우 배열의 최대 길이를 사전에 정의해줘야 한다

```C
#include <stdio.h>

int main(int argc, char * argv[])
{
    char country[3] = "US";
    printf ("%c%c\n", country[0], country[1]);
    printf ("%s\n", country);
    return 0;
}
```

`make a list using python`

- Python의 경우 배열(문자열)의 길이를 사전에 정해주지 않아도 동작한다
- JS또한 길이를 사전에 정해주지 않아도 동작한다
- 이러한 특징 때문에 파이썬과 JS의 배열이 자료구조의 배열과 같다고 볼 수는 없다

```py
country = 'US'
print (country)

>>> US

country = country + 'A'
print(country)

>>> USA
```

`1 차원 배열`

```py
# 1차원 배열: 리스트로 구현시
data_list = [1, 2, 3, 4, 5]

print(data_list)
>>>

[1,2,3,4,5]
```

`2 차원 배열`

```py
# 2차원 배열: 리스트로 구현시
data_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

print(data_list)

[
  [1,2,3],
  [4,5,6],
  [7,8,9]
]
```

<br/>

### 큐

Queue 구조

- 줄을 서는 행위와 유사
- 가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조
- 음식점에서 가장 먼저 줄을 선 사람이 제일 먼저 음식점에 입장하는 것과 동일
- FIFO(First-In, First-Out) 또는 LILO(Last-In, Last-Out) 방식으로 스택과 꺼내는 순서가 반대

<img src="https://camo.githubusercontent.com/a7ee55bf3532f3715605a7e4e5af65ee15822fe0e94a5d414ecfa4059c2e331d/68747470733a2f2f7777772e66756e2d636f64696e672e6f72672f30305f496d616765732f71756575652e706e67" alt="큐">

- 출처: http://www.stoimen.com/blog/2012/06/05/computer-algorithms-stack-and-queue-data-structure/

<img src="https://github.com/junh0328/zero_base_algorithm/raw/main/images/queue.gif" alt="그림으로 보는 큐">

<br/>

#### 알아둘 용어

- Enqueue: 큐에 데이터를 넣는 기능 (JS에서 push)
- Dequeue: 큐에서 데이터를 꺼내는 기능 (JS에서 shift)

<br/>

#### 파이썬 queue 라이브러리 활용해서 큐 자료 구조 사용하기

**queue 라이브러리에는 다양한 큐 구조로 ① Queue(), ② LifoQueue(), ③ PriorityQueue() 제공**

프로그램을 작성할 때 프로그램에 따라 적합한 자료 구조를 사용

Queue(): 가장 일반적인 큐 자료 구조

<details>

```py
# 큐 (Queue)

import queue

# FIFO QUEUE (일반적인 구조의 큐) 사용하기

data_queue = queue.Queue()

print('data_queue:', data_queue)
print('type:', type(data_queue))

print()

# 데이터 삽입 (put)

data_queue.put(1)
data_queue.put(2)
data_queue.put(3)

print('data_queue.qsize():', data_queue.qsize()) >>> 3

print()

# 데이터 추출 (get)

print('data_queue.get():', data_queue.get()) >>> 1
print('data_queue.get():', data_queue.get()) >>> 2
print('data_queue.get():', data_queue.get()) >>> 3

```

</details>

LifoQueue(): 나중에 입력된 데이터가 먼저 출력되는 구조 (스택 구조라고 보면 됨)

<details>

```py
import queue

# LIFO QUEUE (스택과 같은 구조의 큐) 사용하기

data_queue = queue.LifoQueue()

print('data_queue:', data_queue)
print('type:', type(data_queue))

print()
