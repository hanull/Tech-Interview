# PCB & Context Switching

## PCB(Process Control Block)
CPU가 프로세스가 여러개일 때, CPU 스케줄링을 통해 관리를 하는데 이때, CPU는 각 프로세스들이 누군지 알아야 관리가 가능하다.
프로세스들의 특징을 갖고있는 것이 바로 프로세스 메타데이터(Process Metadata)이고, 이 메타데이터는 프로세스가 생성되면 PCB(Process Control Block)이라는 곳에 저장된다.

운영체제가 시스템 내의 프로세스들을 관리하기 위해서 프로세스 정보들을 저장하는 곳을 말한다.
- 보통 PCB는 프로세스의 모든 정적/동적 정보를 보관하는 커널 데이터 구조라고 한다.
- 프로세스 상태 관리, 문맥 교환을 위해 필요하다.
- 프로세스 생성 시 만들어지며 주기억장치에 유지된다.

### PCB에 저장되는 내용들
- process 상태
    - CPU를 할당해도 되는지 여부를 결정하기 위해 필요함
- pc값
    - 다음에 수행할 명령어의 위치를 가리킨다
- CPU register
    - CPU 연산을 위해 현 시점에 레지스터에 어떤 값을 저장하고 있는지를 나타냄
- CPU 스케줄링 정보
- 메모리 관리 정보
- 자원 사용 정보
- 입출력 상태 정보

### PCB가 왜 필요한데?
CPU에서는 프로세스의 상태에 따라 교체작업이 이루어진다. (interrupt가 발생해서 할당받은 프로세스가 wating 상태가 되고 다른 프로세스를 running으로 바꿔 올릴 때)
이때, 앞으로 다시 수행할 대기 중인 프로세스에 관한 저장 값을 PCB에 저장해두는 것이다.

### PCB는 어떻게 관리되나?
Linked List 방식으로 관리한다. PCB List Head에 PCB들이 생성될 때마다 붙게 된다. 즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료시 제거된다.


## 문맥 교환(Context Swithcing)
문맥 교환이란 현재 진행하고 있는 Task(Process, Thread)의 상태를 저장하고 다음 진행할 Task의 상태 값을 읽어 적용하는 과정을 말한다.
즉, CPU를 점유하고 있던 프로세스A가 I/O interrupt, System Call, tile slice burst 등으로 인해 blocked 되고, 다른 프로세스B가 CPU를 점유하게 되는 상황

### Context Switching Cost
Context Switching이 발생하게 되면 많은 Cost가 소요된다.
- Cache 초기화
- Memory Mapping 초기화
- Kernel은 항상 실행되어야 함(메모리의 접근을 위해서)


###  Process vs Thread
Context Switching 비용은 Process가 Thread보다 많이 든다.
- Thread는 Stack 영역을 제외한 모든 메모리를 공유하기 때문
- Context Switching 발생시 Stack 영역만 변경을 진행하면 된다.


### 참고
- https://nesoy.github.io/articles/2018-11/Context-Switching