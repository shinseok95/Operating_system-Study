# Operating System Study
> 운영체제에 대해 공부한 내용을 정리하는 Repository입니다.<br>
> (A. Silberschatz et al., Operating System Concepts, 9th Edition, John Wiley & Sons, Inc. 2013.)

# 목차

- [Instruction](#Instruction)
- [Process](#Process)
- [CPU Scheduling](#CPU-Scheduling)
- [Process Synchronization](#Process-Synchronization)
- [Memory Management](#Memory-Management)
- [Virtual Memory](#Virtual-Memory)
- [File Systems](#File-Systems)


## Instruction

- Program 
  - 명령어의 집합

- Operating System
  - 의미
    - 좁은 의미 : 커널 (메모리에 상주)
    - 넓은 의미 : 커널 + 각종 주변 시스템 유틸리티
  - 목적
    - 시스템의 자원을 효율적으로 관리 (메모리, I/O, 프로세서 등)
    - 컴퓨터를 편리하게 사용할 수 있도록 환경제공

- Interrupt
  - CPU의 제어를 운영체제로 넘기는 것
  - 종류
    - Hardware Interrupt
    - Software Interrupt (Trap) : exception, System Call

- System Call
  - 사용자 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출하는 것

- DMA (Direct Memory Access)
    - I/O의 Interrupt 때문에 CPU Overhead ↑ => DMA가 직접 I/O 데이터를 메모리에 할당

- 컴퓨터 시스템 구조

![aa](https://user-images.githubusercontent.com/48644958/123042648-1888bd80-d432-11eb-9b32-7e64b98ee1c4.png)

- 저장 장치 구조

![bb](https://user-images.githubusercontent.com/48644958/123043029-a6fd3f00-d432-11eb-8167-275d9b2cc022.png)

> [사진 출처](https://programmer-student.tistory.com/8)

## Process

- Process
  - 실행 중인 프로그램

- 프로세스 상태도

![cc](https://user-images.githubusercontent.com/48644958/123043377-2854d180-d433-11eb-8670-6be5780e0ce6.jpeg)
> [사진 출처](https://jhnyang.tistory.com/7)

- PCB (Process Control Block)
  - 운영체제가 각 프로세스를 관리하기 위해 프로세스당 유지하는 정보
  - 구성
    - OS가 관리상 사용하는 정보 (ex : PID)
    - CPU 수행 관련 하드웨어 값 (ex : Program Counter)
    - 메모리 관련 정보 (ex : Code, data, stack 위치정보)
    - 파일 관련 정보 (ex : File description)

- IPC (Interprocess Communication)
  - ① Messaging passing : 커널을 통해 이미지 전송 (send, receive)
  - ② Shared Memory : 서로 다른 프로세스간 일부 주소공간 공유

- Context Switching
  - CPU를 한 프로세스에서 다른 프로세스로 넘겨주는 과정
  - 뺏기는 프로세스의 정보는 해당 PCB에 저장해줌

- Thread
  - 의미 : 프로세스의 CPU 수행 단위
  - 구성
    - Program Counter 
    - Register set
    - Stack space
  - 공유 자원
    - Code Section
    - Data Section
    - OS resource
  - 장점
    - ① 빠름 (프로세스를 만들고 Context switching 하는 것보다 프로세스 내부에서 Thread를 활용하는 것이 5배 빠름)
    - ② 자원 공유
    - ③ 병렬성 ↑

![dd](https://user-images.githubusercontent.com/48644958/123044386-88984300-d434-11eb-9b8e-d6e35e5795b2.jpg)
> [사진 출처](https://m.blog.naver.com/three_letter/220333796848)
> 
## CPU Scheduling

- Scheduler
  - CPU 스케줄을 관리
  - 대기 상태의 프로세스 중 다음에 실행될 프로세스를 고름
  - 방법
    - Nonpreemptive (비선점형) : 실행중인 프로세스가 자진 반납할 때까지 놔둠 (ex : I/O interrupt, terminate 등) -> 물론 time out시에는 빼앗음
    - preemptive (선점형) : 우선 순위인 프로세스가 들어오면 실행중인 프로세스를 강제로 반납시킴
- Dispatcher
  - 스케줄러에 의해 선택된 프로세스에 CPU 제어권을 넘김

- 성능 척도
  - CPU utilizaion (이용률) : 전체 시간 중 CPU가 작동한 비율
  - Throuhgput (처리량) : 단위 시간 중 처리한 양
  - Turnaround time (반환시간) : CPU 쓴 시간 + CPU 기다린 시간
  - Wating time : 기다린 전체 시간
  - Response time : 프로세스가 시작하고, 최초로 CPU를 사용하기까지의 시간

- 스케줄링 알고리즘
  - ① FCFS (First Come First Served)
    - 먼저 온 프로세스 먼저 실행
  - ② SJF (Shortest Job First)
    - CPU 이용시간이 짧은 프로세스 먼저 실행
    - 문제점 : Starvation (기아현상)
  - ③ SRTF (Shortest Remaing Time First)
    - Preemptive 방식의 SJF 알고리즘
    - 중간에 더 짧은 프로세스가 들어오면 Context Switching (현재 남아 있는 시간 기준)
  - ④ Priority Scheduling
    - 우선 순위가 높은 프로세스 먼저 실행
    - 문제점 : Starvation (기아현상)
    - 해결책 : Aging (오래 기다린 프로세스의 우선순위를 높여줌)
  - ⑤ Round Robin
    - 각 프로세스는 할당 시간 (Time Quantum)을 사용하면, Queue의 맨 마지막으로 들어가서 대기
    - 장점 : Response Time이 짧아짐
    - 단점 : Average turnaround time이 길어짐
  - ⑥ Multilevel Queue
    - Ready Queue를 여러 개로 분할 (각 Queue마다 우선순위가 존재)
  - ⑦ Multilevel Feedback Queue
    - 프로세스가 다른 Queue로 이동 가능 ( Aging을 통해 구현)


## Process Synchronization

- Race Condition (경쟁상태)
  - 여러 프로세스들이 동시에 공유데이터에 접근하는 상태
  - 해결 조건
    - ① Mutual Exclusion (상호 배제) : 어떤 프로세스가 사용 중이면, 다른 프로세스는 들어가면 안됨
    - ② Progress (진행) : Critical Section(임계 구역)에 아무도 없을 때, 들어가고싶은 프로세스는 들어갈 수 있어야함
    - ③ Bounded waiting (유한 대기)

- Semaphore (세마포어)
  - 공유 자원에 대한 접근을 제한하는 방법
  - 종류
    - ① Counting Semaphore : Critical Section에 들어갈 수 있는 스레드가 여러개인 세마포어 (즉, 자원이 여러개)
    - ② Binary Semaphore (Mutex) : Lock & Unlock만 가능한 세마포어
  - 함수
    - P(s) : 자원을 획득하는 과정 (Lock)
    - V(s) : 자원을 반납하는 과정 (Unlock)
 
- Monitor (모니터)
  - 하나의 프로세스 내에서 다른 스레드간의 동기화
  - 한 순간에 오직 한 프로세스만이 모니터 내에 존재 가능
  - 장점 
    - 개발자가 세마포어를 통해 복잡한 개발 필요 X => 라이브러리, 프레임워크에서 제공 (ex : Java의 synchronized)

- Deadlock (데드락)
  - 일련의 프로세스들이 서로가 가진 자원을 기다리며 Block된 상태
  - 발생 조건
    - ① Mutual exclusion (상호 배제) : 한 프로세스만 사용
    - ② No preemptive (비선점) : 뺏기지 않음
    - ③ Hold and Wait (보유 & 대기) : 보유 자원을 내놓지 않음
    - ④ Circular wait (환형 대기) : 프로세스간 사이클 형성
  - 해결 방법
    - ① Deadlock Prevention : 발생 조건 4가지 중 어느 하나가 만족되지 않도록 하는 것
    - ② Deadlock Avoidance : 부가적인 정보를 이용해 Deadlock 가능성이 없을 때만 자원 할당
    - ③ Deadlock Detection and Recovery : 데드락이 발생하면 비용을 최소할 프로세스에게서 자원을 빼앗음
    - ④ Deadlock Ignorance : 시스템이 책임지지 않고, 사용자가 알아서 하도록 함 (대부분의 OS가 채택)

## Memory Management

## Virtual Memory

## File Systems
