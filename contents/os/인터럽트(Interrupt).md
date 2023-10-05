# 인터럽트
- CPU에 의해 정상적으로 프로그램이 실행되는 도중 방해를 받아 프로그램이 중단되는 현상자체를 일컫는다.
- 인터럽트가 발생한 경우 해당 인터럽트를 해결하기 위한 작업을 선처리한다.
- 인터럽트 타입에는 **내부(Software)** 인터럽트와 **외부(HardWare)** 인터럽트로 나뉜다.

## 하드웨어 인터럽트
- 일반적으로 인터럽트를 통틀어 지칭하는 명칭
- CPU 외부로부터 인터럽트 요구 신호에 의해 발생되는 인터럽트
- Maskable interrupt와 Non-Maskable interrupt로 분리된다.

### Maskable interrupt
- Interrupt Mask : 인터럽트가 발생하였을 때 요구를 받아들일지 말지 지정하는 것

### Non-Maskable interrupt
- 가장 우선 순위가 높은 인터럽트
- interrupt Mask가 불가능
- 거부, 무시할 수 없음 (매우 중요함)
- 정전, 하드웨어 고장 등 어쩔수없는 오류

### 하드웨어 인터럽트 타입
- 입출력, 정전이나 전원 이상, 기계 착오, 외부신호

## 소프트웨어 인터럽트
- 자신이 실행한 명령 또는 CPU 명령에 의해 발생
- trap 또는 exception이라고 한다.
- 프로그램의 오류에 의해 생기는 인터럽트

### 소프트웨어 인터럽트 타입
- 0으로 나누는 경우
- OverFlow/UnderFlow
- 페이지 부재
- 부당한 기억장소의 참조

## 인터럽트 우선순위
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbXN8JO%2FbtrcrNOCdrX%2Fp9yBaxaFeCQKL7VleUPKWk%2Fimg.png)

## 인터럽트 벡터
- 여러가지 인터럽트에 대해 해당 인터럽트 발생시 처리해야 할 루틴(ISR)의 주소를 보관하고 있는 공간
- 대부분의 CPU들은 인터럽트 벡터 테이블을 가지고 있음
- 인텔x86에서는 이를 IDT(Interrupt Descriptor Table)이라고 한다.
 
## 인터럽트 서비스 루틴
- 인터럽트 핸들러 Interrupt handler 라고도 함
- 인터럽트가 접수되면 각각의 인터럽트에 대응하여 특정 기능을 처리하는 기계어 코드 루틴(커널이 실행)
  - ex) 키보드 자판을 눌러 키보드 인터럽트가 발생하면 이에 해당하는 인터럽트 서비스 루틴이 실행됨

## 인터럽트 과정 
시나리오 : 프로세스 A 실행 중 디스크에서 어떤 데이터를 읽어오라는 명령을 받았을 때

1. 프로세스 A는 system call을 통해 인터럽트를 발생시킴
2. CPU는 현재 진행중인 기계어 코드를 완료
3. 현재까지 수행중이었던 상태를 해당 프로세스의 PCB(Process Control Block)에 저장 (수행중이던 메모리 주소, 레지스터 값 등등)
4. PC(Program Counter, IP)에 다음 실행할 명령의 주소 저장
5. 인터럽트 벡터를 읽고 ISR 주소값을 얻어 ISR(interrupt Service Routine)으로 점프하여 루틴을 실행
6. 해당 코드 실행
7. 해당 일을 다 처리하면 저장했던 프로세스 상태 복구
8.ISR의 끝에 IRET명령어에 의해 인터럽트가 해제
9. IRET 명령어가 실행되면, 대피시킨 PC 값을 복원하여 이전 실행위치로 복원

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsOicV%2FbtrcebCFFGo%2FJOr4V3M4umegWKsqdtSV8K%2Fimg.jpg)