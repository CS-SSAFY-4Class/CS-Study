# PCB와 Context Switching(문맥 교환)
## Process Metadata
프로세스는 컴퓨터에서 연속적으로 실행되고 있는 동적인 상태의 컴퓨터 프로그램, 하나의 작업 단위이다.<br>
프로세스는 여러가지 특징을 가지는데, 이를 Process Metadata라고 한다.

<br>

아래는 Process Metadata의 정보들이다
|Process Metadata|정보|
|---|---|
|Process ID(PID)|프로세스 고유 식별 번호|
|Process State|프로세스의 현재 상태(준비/실행/대기)를 기억|
|Process Priority|프로세스 우선순위 등과 같은 스케줄링 관련 정보 기억|
|CPU Registers|프로세스 레지스터 상태를 저장하는 공간, CPU 내 범용/데이터/세그먼트 레지스터 등이 갖고있는 값을 기억시킴|
|Program Counter|이전에 배운 PC로 다음 작업할 명령어 위치 기억|

<br><hr><br>

## PCB(Porcess Control Block)
Process Metadata를 저장해 놓는 곳, 하나의 PCB 안에는 하나의 프로세스 정보가 담겨있다.<br>
프로그램 실행 -> 프로세스 생성 -> 프로세스 주소 공간(코드, 데이터, 스택)에 생성 -> Process Metadata를 PCB에 저장

<br>

### PCB의 상세 구조
Pointer | Process State
Process Number
Program Counter
Registers
Memory Limits
List of Open Files

- Process State: 프로세스 상태(Create, Ready, Running, Block, Terminated)
- Process Counter: 다음 실행할 명령어의 주소값

<br>

### PCB 필요성과 관리 방법
CPU 내에서 프로세스의 상태에 따라 교체 작업이 이루어진다.<br>
(인터럽트가 발생해 할당받은 프로세스가 BLock 상태가 되고 다른 프로세스를 Running으로 바꿀때)<br>
이 때, 앞으로 다시 수행 할 Block 상태 프로세스의 상태값을 PCB에 저장해둔다.<br>
<br>
이러한 PCB는 Linked List 방식으로 관리된다.
PCB List Head에 PCB들이 생성될때마다 데이터가 하나씩 붙는다.<br>
주소 값으로 연결이 이루어져있는 연결리스트이기 때문에 삽입/삭제가 용이하다.<br>
(프로세스가 생성되면 해당 PCB가 생성되고 완료시 제거된다)<br>
수행중인 프로세스를 변경할 때 CPU의 레지스터 정보가 변경되는 것을 Context Switching이라고 한다.

<br><hr><br>

## Context Switching
멀티 프로세스 환경에서 CPU가 하나의 프로세스를 실행하고 있는 상태에서 인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 떄<br>
기존 프로세스의 상태/레지스터 값을 저장하고 다음 프로세스를 수행하도록 새로운 상태/레지스터 값을 교체하는 작업<br>

CPU는 한번에 하나의 프로세스만 수행할 수 있다. 여러개의 프로세스를 동시에 수행하는 것처럼 보이기 위해서 필요하다.

<br>

### Overhead로 인한 성능 저하
P0, P1 두 프로세스가 있을 때, P0가 실행중인 상태에서 유휴(idle)상태가 될 때 프로세스 P1이 실행되기 까지(Context Switching 시) 1~1000 마이크로초의 지연시간이 존재하는데, 이를 오버헤드라 하고 이 과정에서 CPU는 아무런 일도 하지 못하게 된다.<br>

#### 해결방안

  - 문맥 교환은 OS에서 자주 발생하므로 가능한 적은 자료들은 주기억 장소로 옮겨야 한다
  - 최근의 운영체제들은 효율적인 Context Switching을 위해 프로세스 구성 기법인 쓰레드(Thread)를 이용하고 있다. (프로세스를 다수의 스레드로 구성하여 병행성을 높이고 실행환경을 공유시켜 성능을 개선)
