# System Call
- OS에서 커널 모드를 이용할 시에 OS에서 제공하는 다양한 인터페이스를 `System Call`이라고 한다.
- 프로세스가 하드웨어에 직접 접근하여 필요한 기능을 사용할 수 있도록 해준다.
- 각 시스템 콜은 여러 기능을 제공하며, 고유 번호가 부여된다.

1. 매개변수를 CPU 레지스터 내에 전달한다.
2. 이 경우에 매개변수의 갯수가 CPU 내의 총 레지스터 개수보다 많을 수 있다.
3. 위와 같은 경우에 매개변수를 메모리에 저장하고 메모리의 주소가 레지스터에 전달된다. (아래 그림 참고) 매개변수는 프로그램에 의해 스택(stack)으로 전달(push) 될 수도 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F27118142535CCF060A

2, 3번 방법의 경우 전달되는 매개변수의 개수나 길이에 제한이 없기 때문에 몇몇 운영체제에서 선호하는 방식이다.

메모리를 사용한 매개변수를 전달


## 시스템 콜의 유형
시스템 콜은 여섯 가지의 중요한 범주로 나눌 수 있다.

### 프로세스 제어
- 파일 조작
- 장치 조작
- 정보 유지보수
- 통신
- 보호
**1 프로세스 제어(Process Control)**

끝내기(exit), 중지(abort)
적재(load), 실행(execute)
프로세스 생성(create process) - fork
프로세스 속성 획득과 설정(get process attribute and set process attribute)
시간 대기(wait time)
사건 대기(wait event)
사건을 알림(signal event)
메모리 할당 및 해제 : malloc, free

**2 파일 조작(File Manipulation)**

파일 생성(create file), 파일 삭제(delete file)
열기(open), 닫기(close)
읽기(read), 쓰기(write), 위치 변경(reposition)
파일 속성 획득 및 설정(get file attribute and set file attribute)

**3 장치 관리(Devide Management)**

하드웨어의 제어와 상태 정보를 얻음(ioctl)
장치를 요구(request devices), 장치를 방출release device)
읽기(read), 쓰기(write), 위치 변경
장치 속성 획득, 장치 속성 설정
장치의 논리적 부착(attach) 또는 분리(detach)

**4 정보 유지(Information Maintenance)**

getpid(), alarm(), sleep()
시간과 날짜의 설정과 획득(time)
시스템 데이터의 설정과 획득(date)
프로세스 파일, 장치 속성의 획득 및 설정

**5 통신(Communication)**

pipe(), shm_open(), mmap()
통신 연결의 생성, 제거
메시지의 송신, 수신
상태 정보 전달
원격 장치의 부착 및 분리

**6. 보호(Protection)**

chmod()
umask()
chown()
일반적인 통신 모델에는 메시지 전달과 공유 메모리 두가지가 있다.

메시지 전달 모델에서는 두 프로세스의 통신에 정보 교환을 위한 메시지를 주고 받는다.
공유 메모리 모델에서는 다른 프로세스가 소유한 메모리에 접근을 위해 특정 시스템 콜을 호출한다. 일반적으로 운영체제는 서로 다른 프로세스간의 메모리 접근을 차단한다. 공유 메모리 기법을 사용하기 위해서는 통신하려는 프로세스들이 이러한 차단을 풀어주는데 동의해야한다.