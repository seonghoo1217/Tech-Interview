# Data Structure -1

- [Array vs Linked List](#Array_vs_Linked_List)
- [HashTable](#HashTable)

***************************************

## Array vs Linked List

### Array

가장 기본적인 자료구조에 속하며, **연속된 메모리 공간**에 순차적으로 데이터를 저장하는 선형 자료구조이다.
배열의 가장 큰 특징으로는 `색인(index)`으로 해당 원소(element)를 접근할 수 있다는 점과 논리적 저장 순서와 물리적(메모리) 저장 순서가 일치한다.

접근할 때의 시간 복잡도는 `Big-O(1)`에 해당 하며 즉,비순차접근(Random Access)가 가능하다는 장점이 존재한다.

![Array](https://velog.velcdn.com/images%2Fcodenmh0822%2Fpost%2F36069838-32b5-460f-ad1e-706af189bcdc%2Fimage.png)

- 배열의 맨 뒤 데이터를 삽입 또는 삭제하는 경우 : O(1)

![time](https://velog.velcdn.com/images%2Fcodenmh0822%2Fpost%2F2a09cfb9-0d13-4b31-a4a9-fc9b8e216b46%2Fimage.png)

**배열의 끝 주소 = 시작주소 + (1칸이 차지하는 주소 X 배열 길이)**

위 수식을 통해 배열의 끝 주소를 찾고, 배열의 길이를 1 증가시킨 후, 추가할 원소 데이터를 저장하면 된다.

그러므로 시간복잡도는 O(1)이다. 

- 배열의 맨 뒤를 제외한 경우의 위치에 데이터를 삽입 / 삭제 하는 경우 : O(N)

![img.png](img/array_insert.png)

정확히 임의의 위치에 원소를 새로 추가하기 위해 `Big-O(1)`가 소요되지만 요소의 개수를 N개로 가정하였을 때 통상적으로 Big-O(N)으로 표기한다.

정확히 중간에 삽입 또는 삭제하는 경우에도 N/2로 가정하여 O(N)으로 간주된다.

![array_delete](img/array_delete.png)

유의할 점으로는 만약 배열의 원소 중 어느 원소를 삭제했다고 했을 때, 배열의 연속적인 특징이 깨지게 된다.
배열의 빈공간이 생겨 특성이 깨지게된다. 따라서 삭제한 원소보다 큰 인덱스를 가지는 원소들을 `shift`해줘야하는 비용이 발생한다.

이 경우에는 시간복잡도가 Big-O(n)에 해당된다. 그렇기 때문에 배열에서의 삭제기능에서 worst case 시간복잡도는 O(n)이 된다.

삽입의 경우도 만약 첫번째 자리에 새로운 원소를 추가하고자 한다면 모든 원소들의 인덱스를 1 씩 shift 해줘야 하므로 이 경우도 O(n)의 시간을 요구하게 된다.

### Linked List
해당 문제점을 해결하기 위해 고안된 자료구조가 연결리스트라고 불리는 Linked List이다. 각각의 원소들은 자기 자신 다음에 어떤 원소인지만을 기억하고 있다.
즉, 하나의 노드가 다음 노드를 기억하고 있기에 삽입 또는 삭제 작업을 할경우 시간복잡도는 `Big-O(1)`이다

하지만, Linked List의 고질적인 문제점으로 지적되는 원하는 위치의 삽입 작업을 하기위해 첫 요소부터 Search 작업을 수행하게 된다.
Array와는 달리 논리적 저장 순서와 물리적 저장순서의 차이가 존재하기 때문이다.

만약 길이가 5인 List의 3번째 요소 중간에 새로운 요소를 삽입할 경우 삽입후 원래 요소의 순서와 비교하며 새롭게 정렬을 시도하기 때문에, 새로운 삽입은
결국 삽입 후 정렬이 일어나게되고 삭제 또한 마찬가지기에 추가적으로 시간복잡도 `Big-O(n)`을 가지게 된다.

그 결과 linked list 자료구조는 search 에도 O(n)의 time complexity 를 갖고, 삽입, 삭제에 대해서도 O(n)의 time complexity 를 갖는다.
하지만 Tree 구조에서 유용성이 존재하여 지향하는 자료구조는 아니며, Tree 구조의 근간이 되는 자료구조이다.

*****************

## HashTable

`Hash`는 내부적으로 `배열`을 이용하여 데이터를 저장하기에 빠른 접근속도를 가진다.
특정한 값을 Search 할때 데이터 고유의 **인덱스**에 접근하게되어 평균적인 시간 복잡도는 `Big-O(1)`에 해당한다.

하지만, 이 인덱스로 저장되는 `Key`값이 불규칙한 값이 들어가게된다.

그래서 HashTable의 경우 개발자가 **독단적인 알고리즘을 이용하여** **저장할 데이터와 연관된 고유의 숫자를 만들어 낸 후** 이를 인덱스로 사용한다.
정 데이터가 저장되는 인덱스는 그 데이터만의 고유한 위치이기 때문에, 삽입 연산 시 다른 데이터의 사이에 끼어들거나, 삭제 시 다른 데이터로 채울 필요가 없으므로 연산에서 추가적인 비용이 없도록 만들어진 구조이다.

### HashTable 개념요약

- Key와 Value를 1:1로 연관지어 저장하는 자료구조(연관배열 구조)
- Map과 유사한 성격을 띄고 있으나 차이점이 존재
- Key를 이용하여 Value를 도출한다.

### HashTable 기능

- 연관배열 구조와 동일한 기능의 지원
  - Key, Value가 주어졌을 때, 두 값을 저장
  - Key가 주어졌을 때, 해당 Key에 연관된 Value 조회
  - 기존 Key에 새로운 Value가 주어졌을 때, 기존 Value를 새로운 Value로 대체
  - Key가 주어졌을 때, 해당 Key에 연관된 Value 제거

### HashTable 구성도

![HashTable](img/hashTable.png)

- Key,Hash Function,Hash,Value,저장소(Bucket,Slot)으로 구성

### Key
- 고유한 값이다.
- 저장 공간의 효율성을 위해 Hash Function에 입력하여 Hash로 변경 후 저장
  - Key는 길이가 다양하기에 그대로 저장할 경우 다양한 길이만큼의 저장소 구성이 필요하다.

### Hash Function
- Key를 Hash로 바꿔주는 역할을 수행한다.
- 해시 충돌(서로 다른 Key가 같은 Hash가 되는 경우)이 발생할 확률을 최대한 줄이는 함수를 만드는 것이 중요

### Hash
- Hash Function의 결과
- 저장소에 Value와 매칭되어 저장된다.

### Value
- 최종적으로 저장소에 저장되는 값
- 키와 매칭되어 삭제,저장,검색 작업 가능

### HashTable의 동작과정

1. Key를 HashFunction을 통해 Hash로 생성한다.
2. Hash를 배열의 index로 사용한다.
3. 해당 Index에 Value를 저장한다.

* HashTable 크기가 10이라면 A라는 Key의 Value를 찾을 때 hashFunction("A") % 10 연산을 통해 인덱스 값 계산하여 Value 조회

### Hash 충돌
- 서로다른 Key가 Hash Function에 의해 중복적인 Hash를 산출
- 충돌이 많아질 수록 탐색의 시간복잡도가 O(1)에서 O(n)으로 증가

### Hash 충돌 해결방법

1. **Separating Chaining**
- JDK 내부에서 사용하는 충돌처리 방식
- 추가적인 메모리를 사용하여 동일한 버킷에 값이 있으면 Linked List로 해당 value를 뒤에 저장한다.

![Separating Chaining1](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/675px-Hash_table_5_0_1_1_1_1_1_LL.svg.png)

![Separating Chaining2](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Hash_table_5_0_1_1_1_1_0_LL.svg/750px-Hash_table_5_0_1_1_1_1_0_LL.svg.png)

- 자바 8이상에서는 데이터의 크기에 따라 Linked List 대신 Tree를 사용하며, Tree의 사용이 성능상 이점이 더 높음
  - Linked List 데이터 6개 이하, Red-Black Tree 데이터 8개 이상
- Linked List 사용시 충돌이 발생하면 충돌 발생한 인덱스가 가리키고 있는 Linked List에 노드를 추가하여 삽입한다.
- Key에 대한 Value 탐색 시에는 인덱스가 가리키고 있는 Linked List를 선형 검색하여 Value 반환 (삭제도 마찬가지)
- Linked List 구조를 사용하기 때문에 추가 데이터 수 제약이 적은편

2. **Open Addressing**
- 추가 메모리 공간을 사용하지 않고, HashTable 배열의 빈공간을 이용하는 방법
- 데이터 삽입시 해당 버킷(target)이 사용되고 있다면, 다른 해시 버킷에 데이터를 삽입하는 방식
- 데이터를 저장,조회하는 방식이 다양하다.
- Separating Chaining 방식에 비해 적은 메모리 사용
- 방법은 Linear Probing, Quadratic Probing, Double Hashing
- 삭제 작업에 유의

3. Resizing
- 저장 공간이 일정 수준 채워지면, Separating Chaining의 경우 성능 향상을 위해,Open addressing의 경우 배열크기의 확장을 위해 Resizing
- 보통 두배로 확장시킨다.
- 확장 임계점은 현재 데이터 개수가 Hash Bucket 개수의 75%가 될 때

### HashTable의 장점
- 적은 리소스로 많은 데이터를 효율적으로 관리 가능
  - ex. Cloud에 있는 많은 데이터를 Hash로 매핑하여 작은 크기의 시 메모리로 프로세스 관리 가능
- 배열의 인덱스를 사용하기 때문에 빠른 검색,삭제,삽입 능력을 가지며 시간복잡도는 O(1)
- Key와 Hash사이의 연관성이 존재하지 않기에 보안에 유리하다.
- 데이터 캐싱에 많이 사용
  - get,put 기능에 캐시 로직 추가 시 자주 hit하는 데이터 바로 검색 가ㅡㄴㅇ
  - 중복 제거에 유용

### HashTable 단점
- 충돌 발생 가능성
- 공간 복잡도 증가
- 순서 무시
- 해쉬 함수에 의존적

## HashTable vs HashMap
- Key-Value 구조 및 Key에 대한 Hash로 Value 관리하는 것은 동일

- HashTable
  - 동기처리(thread-safe)
  - Key-Value 값으로 null 미허용 (Key가 hashcode(), equals()를 사용하기 때문)
  - 보조 Hash Function과 separating Chaining을 사용해서 비교적 충돌 덜 발생 (Key의 Hash 변형)

- HashMap
  - 비동기 처리(멀티스레드에서 사용시 주의해야한다.)
  - Key-Value 값으로 null 허용
  
### HashTable 성능

| |평균|최악|
|----|----|----|
|탐색|O(1)|O(N)|
|삽입|O(1)|O(N)|
|삭제|O(1)|O(N)|