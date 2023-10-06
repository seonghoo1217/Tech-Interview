# Process Management
- CPU에 의해 메모리에 적재된 프로세스가 여러개일 때  CPU 스케줄링을 통해 관리하는 것을 말함
- CPU는 각 프로세스를 관리하기 위해 고유한 식별자 값을 알아야하며, 이를 프로세스의 특징을 가지고 있는 `Process Metadata`를 통해 관리한다.

## Process MetaData
- Process ID
- Process State
- Process Priority
- CPU Registers
- Owner
- CPU Usage
- Memeory Usage

해당 메타데이터는 프로세스가 생성되, **PCB**에 저장

## PCB(Process Control Block)
-  Process Metadata들을 저장해 놓는곳
  - 따라서 PCB에는 Process Metadata인 Process ID, State, Priority, etc...등이 저장이 되어진다.
- 한 PCB에는 한 Process의 정보가 다 담겨있으므로 한 PCB를 보면 그에 해당하는 Process가 어떠한 상태인지 어디 있는지 등등을 알 수 있다.
  - 구조체의 형태를 띄고 있음

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F25673A5058F211C224)

- Program이 실행되면 Process가 생성되게되고 Process Address Space에 Process의 구조에 해당하는 **code,data,stack**이 만들어짐
- 이 Process의 Metadata들은 PCB에 저장
- 따라서 Process Management란 말은 곧 PCB Management란 말과 의미가 일치한다.

> 💡PCB 흐름
> 프로그램 실행 → 프로세스 생성 → 프로세스 주소 공간에 (코드, 데이터, 스택) 생성
> → 이 프로세스의 메타데이터들이 PCB에 저장

### PCB 존재 이유
- CPU에서는 프로세스의 상태에 따라 교체작업이 이루어진다. (interrupt가 발생해서 할당받은 프로세스가 waiting 상태가 되고 다른 프로세스를 running으로 바꿔 올릴 때)
- 이때, 앞으로 다시 수행할 대기 중인 프로세스에 관한 저장 값을 PCB에 저장하기 위함

### PCB 관리 방법
- 연결리스트 방식으로 이를 관리함
- ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F2238664D58F212E331)
- Process가 생성되면 해당 Process의 PCB가 만들어지게되고 그 PCB는 PCB List Head에 붙게된다.
- Process가 종료되면 PCB도 Link List에서 unlink
- 이렇게 수행 중인 프로세스를 변경할 때, CPU의 레지스터 정보가 변경되는 것을 `Context Switching`이라고 한다.

## Context Switching
- CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에 읽어 레지스터에 적재하는 과정
- 보통 인터럽트가 발생하거나, 실행 중인 CPU 사용 허가시간을 모두 소모하거나, 입출력을 위해 대기해야 하는 경우에 Context Switching이 발생한다.
- 프로세스가 **"Ready → Running"**, **"Running → Ready"**, Running → Waiting처럼 상태 변경 시 발생한다.

### Context Swithcing의 OverHead
- 프로세스를 수행하다가 입출력 이벤트가 발생해서 대기 상태로 전환시킴
  - 이때, CPU를 그냥 놀게 놔두는 것보다 다른 프로세스를 수행시키는 것이 효율적
- 즉, CPU에 계속 프로세스를 수행시키도록 하기 위해서 다른 프로세스를 실행시키고 Context Switching 하는 것
- CPU가 놀지 않도록 만들고, 사용자에게 빠르게 일처리를 제공해주기 위한 것이다.