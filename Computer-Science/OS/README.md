## [프로세스 & 스레드](#프로세스-&-스레드)
- 프로세스와 스레드를 비교 설명해주세요.
- 멀티 프로세스, 멀티 스레드, 멀티 코어의 개념을 비교해주세요.

## [인터럽트](#인터럽트)
- 인터럽트가 필요한 이유는?
- 인터럽트가 필요한 이유는?

## [시스템 콜](#시스템-콜)
- 시스템 콜이란?
- 시스템 콜을 사용하는 이유를 설명해주세요.

## [PCM](#PCB)
- PCB란?
- PCB가 필요한 이유를 설명해주세요.
- PCB는 어떻게 관리되는가?

## [Context Switching](#Context-Switching)
- Context Switching 이란?
- Context Switching의 Overhead란?

## [IPC](#IPC)
- IPC란?
- IPC 종류를 3가지 이상 말헤주세요.

## [상호배제](#상호배제)
- 상호배제란 무엇인가요?
- 세마포어와 뮤텍스를 비교 설명해주세요.

## [교착 상태](#교착상태)
- 교착 상태에 대해서 설명해주세요.
- 교착 상태의 발생 조건 4가지는 무엇인가요?
- 교착 상태를 해결할 수 있는 방법은 어떤 것이 있을까요?

## [스케줄링](#스케줄링)
- 스케줄링이란 무엇이고, 어떤 목적으로 사용되나요?
- 선점 스케줄링과 비선점 스케줄링은 어떤 차이를 갖나요?
- 스케줄링 알고리즘에는 어떤 것이 있나요? 해당 알고리즘을 아는대로 설명해주세요.

## [메모리](#메모리)
- 메모리란?
- 논리주소(Logical Address)와 물리주소(Physical Address)를 비교 설명해주세요.
- MMU(Memory Management Unit)에 대해 설명해주세요.
- MMU안에 존재하는 레지스터(Relocation/Limit Register) 에 대해 설명해주세요.
- cpu가 346번지에 있는 내용을 요청했을 때, 어떻게 동작하는지, 어느 위치에서 내요을 가져오는지 설명해주세요. (단, relocation register의 값은 14000이다.)
- limit register가 존재하는 이유는 무엇일까요?

## [단편화](#단편화)
- 외부 단편화란?
- 연속 메모리 할당 방식에 대해 설명해주세요.
- Compaction 방식에 대해 설명해주세요.
- Compaction 방식의 문제점은 무엇일까요?

## [페이징 & 세그먼테이션](#페이징-&-세그먼테이션)
- 페이징과 세그먼테이션이 필요한 이유를 말하시오
- 페이징과 세그먼테이션의 장단점을 비교하시오
- 페이지 교체 알고리즘 종류와 간단한 설명을 하시오
- 페이지 교체 알고리즘 중 FIFO알고리즘의 문제점에 대해 설명하시오


## 프로세스 & 스레드
### 💡 프로세스와 쓰레드를 비교 설명해주세요.
- 프로세스
    - 메모리에 올라와서 실행되고 있는 프로그램의 인스턴스를 말한다.
    - 특징
        - 운영체제로부터 독립된 메모리 영역을 할당받는다.
        - 독립적이기 때문에 통신을 하기 위해서는 IPC를 사용해야 한다.
        - 최소 1개의 쓰레드를 가지고 있다.
- 스레드
    - 프로세스 내에서 할당받은 자원을 이용해 동작하는 실행 단위를 말한다.
    - 특징
        - 프로세스 내에 존재하고, 프로세스가 할당받은 자원을 이용하여 실행된다.
        - 쓰레드는 프로세스 내에서 Stack만 따로 할당 받고, Code, Data, Heap 영역은 공유한다.(Stack을 분리한 이유는 Stack에는 함수의 호출 정보가 저장되는데, Stack을 공유하면 LIFO 구조에 의해 실행 순서가 복잡해지기 때문에 실행 흐름을 원활하게 만들기 위함이다.)
        - 쓰레드는 프로세스의 자원을 공유하기 때문에 다른 쓰레드에 의한 결과를 즉시 확인할 수 있다

### 💡 멀티 프로세스, 멀티 스레드, 멀티 코어의 개념을 비교해주세요.
- 멀티 프로세스
    - 하나의 프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 1개의 작업을 처리하도록 하는 것이다.
    - 특징
        - 1개의 프로세스가 죽어도 자식 프로세스 이외의 다른 프로세스들은 계속 실행된다.
        - Context Switching을 위한 오버헤드(캐시 초기화, 인터럽트 등)가 발생한다.
        - 프로세스는 각각 독립적인 메모리를 할당받았기 때문에 통신하는 것이 어렵다.
- 멀티 쓰레드
    - 하나의 프로그램을 여러 개의 쓰레드로 구성하여 각 쓰레드가 1개의 작업을 처리하도록 하는 것이다.
    - 특징
        - 프로세스를 위해 자원을 할당하는 시스템콜이나 Context Switching의 오버헤드를 줄일 수 있다.
        - 쓰레드는 메모리를 공유하기 때문에, 통신이 쉽고 자원을 효율적으로 사용할 수 있다.
        - 하나의 쓰레드에 문제가 생기면 전체 프로세스가 영향을 받는다.
        - 여러 쓰레드가 하나의 자원에 동시에 접근하는 경우 자원 공유(동기화)의 문제가 발생할 수 있다.


## 인터럽트
### 💡 인터럽트란?
- 실행중인 프로그램을 중단하고 우선순위가 높은 프로그램에게 CPU를 할당하여 실행하는것을 말한다.

### 💡 인터럽트가 필요한 이유는?
- CPU와 I/O의 속도 차이를 극복하기 위해 인터럽트가 필요(입출력 연산이 CPU 명령 수행속도보다 현저히 느리기 때문이다.)
- CPU가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치나 예외상황이 발생하여 처리가 필요한 경우에 발생한다.


## 시스템 콜
### 💡 시스템 콜이란?
- 커널 영역의 기능을 사용자 모드가 접근하게 도와주는 기능을 시스템 콜이라고 한다.

### 💡 시스템 콜을 사용하는 이유를 설명해주세요.
- 유저 애플리케이션이 운영체제의 치명적인 권한(데이터 수정/삭제)를 막기 위해서 사용한다.
- 따라서 직접적인 하드웨어 요청이나 기타 시스템 요청은 운영체제가 제공하는 시스템 콜을 통해서 호출하도록 제공한다.


## PCB
### 💡 PCB란?
- 운영체제가 프로세스를 제어하기 위해서 정보를 저장해놓은 곳. 프로세스의 상태 정보를 저장하는 구조체이다.

### 💡 PCB가 필요한 이유를 설명해주세요.
- 프로세스의 상태 관리, 문맥 교환(Context Switching)을 위해 필요하다.

### 💡 PCB는 어떻게 관리되는가?
- Linked List 방식으로 관리한다.
- PCB List Head에 PCB들이 생성될 때마다 붙게 된다. 주소값으로 연결이 이루어져 있는 연결리스트이기 때문에 삽입 삭제가 용이하다.
- 즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료시 제거된다.


## Context Switching
### 💡 문맥 교환(Context Switching) 이란?
- 문맥 교환이란 CPU가 이전의 프로세스 상태를 PCB에 보관하고, 다음 프로세스의 정보를 PCB에 읽어서 적재하는 과정을 말한다.

### 💡 Context Switching의 Overhead란?
문맥 교환에 소요되는 시간은 시스템 입장에서 볼 때 일종의 오버헤드라고 할 수 있다. 따라서 타이머 인터럽트 시간을 너무 짧게하면 프로세스간 문맥 교환이 너무 자주 일어나 오버헤드가 커지게 된다.


## IPC
### 💡 IPC란?
프로세스는 독립적으로 실행된다. 독립되어있다는 것은 다른 프로세스에게 영향을 받지 않는다는 것이다. 이런 독립적 구조를 가진 프로세스 간의 통신을 해야 하는 상황이 있을 것이고, 이를 가능하도록 해주는 것이 IPC 통신이다. 즉, `내부 프로세스들 끼리 통신을 하는 것`을 말한다.

### 💡 IPC의 종류를 3가지 이상 말해주세요.
- PIPE
- Named PIPE
- Message Queue
- Shared Memory
- Memory Map
- socket


## 상호배제
### 💡 상호배제란 무엇인가요?
- 여러 프로세스나 쓰레드가 공유 자원에 접근하는 것

### 💡 세마포어와 뮤텍스를 비교 설명해주세요.
- 세마포어는 count를 주어 count 값만큼 프로세스/스레드가 접근 가능하도록 하는 기법
- 뮤텍스는 lock/unlock으로 권한을 가진 프로세스/스레드만 접근할 수 있도록하는 기법


## 교착상태
### 💡 교착 상태에 대해서 설명해주세요.


### 💡 교착 상태의 발생 조건 4가지는 무엇인가요?


### 💡 교착 상태를 해결할 수 있는 방법은 어떤 것이 있을까요?


## 스케줄링
### 💡 스케줄링이란 무엇이고, 어떤 목적으로 사용되나요?


### 💡 선점 스케줄링과 비선점 스케줄링은 어떤 차이를 갖나요?

### 💡 스케줄링 알고리즘에는 어떤 것이 있나요? 해당 알고리즘을 아는대로 설명해주세요.


## 메모리
### 💡 메모리란?
주소 덩어리, 인덱싱 할 수 있는 큰 주소 배열

### 💡 논리주소(Logical Address)와 물리주소(Physical Address)를 비교 설명해주세요.
- 논리주소(Logical Address)
    - CPU가 보는 주소
    - 프로세스마다 독립적으로 가지는 주소 공간
    - 각 프로세스마다 0번지부터 시작
- 물리주소(Physical Address)
    - 메모리에 실제 올라가는 위치

### 💡 MMU(Memory Management Unit)에 대해 설명해주세요.
Logical Address 를 Physical Address 로 매핑해주는 하드웨어 장치를 말한다.

### 💡 MMU안에 존재하는 레지스터(Relocation/Limit Register) 에 대해 설명해주세요.
- Relocation Register (Base Register) : 접근할 수 있는 물리적 메모리 주소의 최소값
- Limit Register : 논리적 주소의 범위
### 💡 cpu가 300번지에 있는 내용을 요청했을 때, 어떻게 동작하는지, 어느 위치에서 내요을 가져오는지 설명해주세요. (단, relocation register의 값은 14000이다.)

### 💡 limit register가 존재하는 이유는 무엇일까요?
불법 접근으로 다른 데이터를 가져오는 것을 막기 위해


## 단편화
### 💡 외부 단편화란?
외부 단편화는 메모리에 프로세스가 할당될 만큼 충분한 공간이 존재하지만 공간이 쪼개어져서 프로세스를 넣을 수 없는 것을 말한다.

### 💡 연속 메모리 할당 방식에 대해 설명해주세요.
- 최초 적합(First-fit)
    - 순차적으로 탐색하여 제일 먼저 발견한 적절하게 들어갈 수 있는 곳을 찾아 프로세스를 적재하는 방법
- 최적 적합(Best-fit)
    - 제일 적절하게 들어갈 수 있는 곳을 찾아 프로세스를 적재하는 방법
- 최악 적합(Worst-fit)
    - 크기와 제일 안 맞는 공간(프로세스보다 큰 메모리 공간 중에서)에 프로세스를 넣는 방식

### 💡 Compaction 방식에 대해 설명해주세요.
빈 공간을 한 곳으로 모으는 방식이다.

### 💡 Compaction 방식의 문제점은 무엇일까요?
한 곳으로 모으기 위해서는 메모리를 움직여야 하는데 이 때 발생하는 비용이 크고, 어느 빈 공간을 움직이는 것이 좋은지에 관한 최적 알고리즘이 존재하지 않는다.


## 페이징 & 세그먼테이션
### 💡 페이징과 세그먼테이션이 필요한 이유를 말하시오
- 

### 💡 페이징과 세그먼테이션의 장단점을 비교하시오
- 페이징 기법을 사용하게되면 하나의 프로세스가 사용하는 메모리 공간이 연속적이어야 한다는 제약을 없애 외부 단편화 문제점을 해결할 수 있습니다.
- 하지만 그만큼 Mapping 과정 또한 늘어나기 때문에 Trade-Off 가 발생할 수 있습니다. 그리고 보통 페이지 단위에 알맞게 꽉채워 쓰는게 아니므로 내부 단편화 문제는 여전히 있습니다.


### 💡 페이지 교체 알고리즘 종류와 간단한 설명을 하시오
-

### 💡 페이지 교체 알고리즘 중 FIFO알고리즘의 문제점에 대해 설명하시오
- 