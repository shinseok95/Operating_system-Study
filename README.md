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

## Process Synchronization

## Memory Management

## Virtual Memory

## File Systems
