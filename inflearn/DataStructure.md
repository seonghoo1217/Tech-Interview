# DataStructure

해당 파일은 인프런의 `기출로 대비하는 개발자 전공면접`강의를 수강하며 정리한 글이며, 기존의 정리 글과는 차이가 존재합니다.

## Q. Array는 어떤 자료구조인가요?

Array는 **연관된 data**를 메모리상에 `연속적`이며 `순차적`으로 미리 할당된 크기만큼 저장하는 자료구조

> ✏ Tip
> 
> Array 관련 질문시에는 매우 높은 확률로 linked List에 대한 질문도 따라나온다.
> 이때 Array와 Linked List의 차이점을 중점으로 설명해야하며 가장 큰 차이점으로는 내부 API 사용시 시간복잡도 차이가존재한다.
> 배열의 경우 삽입 또는 삭제의 과정이 맨앞이나 맨뒤가 아닐경우 시간복잡도가 O(N)까지 늘어나지만 Linked List는 하나의 노드가 다음 노드의 정보를
> 가지고 있기에 시간복잡도가 O(1)로 나옴

### Array

- 배열은 저장이 될때 연속적으로 저장되며 중간에 빈자리가 생기지 않는다.
- 고정된 저장 공간을 가진다.

### Array의 Operation들의 time complexity

- 조회 : O(1) randomAccess
  - 주소값을 알고있기에 계산을통해 접근한다. 이를 RandomAccess라고한다.
- 마지막 인덱스에 추가/삭제 : O(1)
- 일반 삽입/삭제 : O(N)
  - 중간에 데이터를 삽입 또는 삭제할 경우 배열내부적으로 이동이 있어야함으로 N의 시간복잡도를 가짐
- 탐색 : O(N)
  - 일일히 탐색을 해야함으로 탐색하고자하는 대상에 따라 시간이 다르므로 N의 시간복잡도를 가진다.

Array의 장점으로는 조회가 빠르다는 점으로 조회가 빈번히 사용되는 작업에는 Array자료구조를 사용한다.
반면, 단점으로는 고정된 크기 특성상 미리 선언하여야하며, 메모리의 낭비나 추가적인 OverHead를 유발할 수 있다.

### Array (꼬꼬무문답) Q. 미리 예상한것보다 더많은 수의 data를 저장하느라 Array의 Size를 넘어서게 되었을 경우 어떻게 해결할 수 있을까요?

기존의 배열보다 더큰 Size의 Array를 선언하여 데이터를 옮겨 할당하고, 모든 데이터를 옮겼다면 기존 Array는 삭제합니다.
이렇게 동적으로 배열의 크기를 조절하는 자료구조를 Dynamic Array라고 합니다.
다른 방법으로는, Array대신 Linked List를 사용함으로서 데이터 추가시 새로운 메모리 공간을 할당받는 방법을 이용합니다.


## Q. Dynamic Array는 어떤 자료구조 인가요?

Array의 경우 Size가 고정되어 선언시 설정한 Size 이상의 데이터를 삽입할경우 저장 불가 또는 대체해야하는 단점이
존재하였습니다. 이를 반해 Dynamic Array는 저장공간이 가득차게 될 경우 resize를 이용하여 유동적으로 size를 조절하여 데이터를 저장하는 자료구조입니다.

> ✏ Tip
> Array의 특징중에 fixed-size의 한계점을 보안하고자 고안된 자료구조인 Dynamic Array
> 중점적으로 언급할 부분은 총두가지로 아래와같다.
> 
> `1.resize를 하는 방식`
>
> `2.데이터를 추가(append)할 때의 시간복잡도`

### Dyamic Array

- Dynamic Array는 정의적으로 size를 자동적으로 resizing을 하는 Array이다.
- 기존 고정된 size를 가진 Static Array의 한계점을 보완하고자 고안되었다.
- Dynamic Array는 data를 계속 추가하다가 기존 할당된 memory를 초과할 경우, size를 늘린 배열을 선언하고 그곳으로 모든 데이터를 이전하여 
최종적으로 기존의 size보다 큰 Array를 가지게되며 이를 `resize`라고 명명한다.
- Dynamic Array의 장점으로는 size가 고정적이지 않기에 이에대한 고려가 없다는 점이 존재한다.
- resizing을 하는방법으로는 `Array Doubling` 또는 `Amortized Analysis`가 존재한다.


### Array Doubling

resizing의 대표적인 방법으로 데이터를 추가(append O(1))하다가 메모리 초과시 기존 배열 size의 두배 크기의 배열을 선언한 후,
데이터를 일일이 옮기는 방법.

이때 데이터의 개수를 N이라고 가정하였을 때 모든 데이터를 옮겨야함으로 시간복잡도는 `O(N)`이 된다.

### 분활상환 시간복잡도 Amortized time complexity

Dynamic Array는 데이터를 추가할 때마다 시간복잡도는 O(1)이 소요된다.
그리고 resizing을 하기 위해선 미리 선언한 size를 넘어가는 순간 일일이 데이터를 모두 옮겨야하고 이때 결과적으로 O(N)의 시간이 걸린다.

**그렇다면 과연 데이터 삽입(append)의 시간복잡도는 O(1)이 맞는가?**

append의 총 과정을 살펴보자면 데이터를 마지막 인덱스에 추가하는 일반적인 작업(시간복잡도 O(1)을 가지는)이 대부분이고, size를 넘어설 때
doubling을 통해 옮기는 과정에서 (resize O(N))이 아주 가끔 발생한다. 
그렇기에 삽입의 시간복잡도는 O(1)이며 정확히는 `amortized O(1)`이라고 한다.

### Amortized Analysis

doubling 과정으로 인해 발생하는 시간복잡도 O(N)을 append operation 자체의 시간복잡도로 보기보다는 평균 연산을 고려하는 방법이다.

몇가지 특징으로는 아래와 같다.

- worst case를 분석한다.
- 연속해서 연산이 발생할 때,최악의 경우의 평균 연산을 고려한다.
- Average Analysis와의 차이점
  - Average Analysis의 경우 확률을 이용한 계산을 사용하지만, Amortized Analysis의 경우 최악의 경우의 평균을 사용한다.


#### Dynamic Array (꼬꼬무 문답) Q. Dynamic Array를 Linked List와 비교하여 장단점을 설명해 주세요.

Linked List와 비교했을 때, Dynamic Array의 **장점**은 다음과같다.

- Dynamic Array도 Array의 성질을 가지기에 데이터 접근 및 할당이 O(1)으로 굉장히 빠르다.
- Dynamic Array의 맨 뒤 데이터를 추가하거나 삭제하는 것 또한 Array의 특성이 있으므로 빠름

Linked List와 비교했을 때, Dynamic Array의 **단점**은 다음과같다.

- Dynamic Array의 맨끝이 아닌 곳에서 data를 insert or remove할 때 느리다.
  - 데이터의 수만큼 shift 해야하기에 시간복잡도 O(N)
- resize를 수행할 때 낮은 performance 발생
- resize에 시간이 많이 걸리고, memory 공간을 필요이상으로 할당받아 메모리 낭비 발생우려 

