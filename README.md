# Operating System Study
> 운영체제에 대해 공부한 내용을 정리하는 Repository입니다.
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
    - 
- 컴퓨터 시스템 구조

![aa](https://user-images.githubusercontent.com/48644958/123042648-1888bd80-d432-11eb-9b32-7e64b98ee1c4.png)

- 저장 장치

![bb](https://user-images.githubusercontent.com/48644958/123043029-a6fd3f00-d432-11eb-8167-275d9b2cc022.png)

> [사진 출처](https://programmer-student.tistory.com/8)

## Process

## CPU Scheduling

## Process Synchronization

## Memory Management

## Virtual Memory

## File Systems
