# 프로세스 스케줄링 & CPU 스케줄링

## 스케줄러 / 스케줄링이란?

![image](https://github.com/user-attachments/assets/183970db-efd4-4deb-bca6-f70882b8ffda)

- 위 그림과 같이 프로그램이 하나만 쭈욱 작동하는 것이 아닌, 프로그램 하나가 잠시 실행되었다가 다시 다른 프로그램으로 스위칭 되는 것을 볼 수 있다.
- 이렇게 스위칭되면서 작업되는 것이 우리 눈에는 여러 개의 프로그램이 동시에 실행되는 것처럼 보이는 것이다.

그렇다면 어떤 기준으로 스위칭 되는 것 일까? 이 기준을 운영체제의 스케줄러(scheduler)가 결정하고 기준에는 **여러가지 알고리즘**들이 있다.

## **스케줄링 방식**

스케줄링에는 크게 **선점형(Preemptive) 스케줄링**과 **비선점형(Non-Preemptive) 스케줄링** 2가지 방식으로 나뉜다.

### **2.1) 선점형(Preemptive) 스케줄링**

프로세스가 CPU를 할당받아 실행 중이더라도 I/O나 인터럽트가 발생한 것도 아니고 모든 작업을 끝내지도 않았는데, 다른 프로세스가 CPU를 강제로 빼앗을 수 있는 방식이다.

CPU 처리 시간이 매우 긴 프로세스가 CPU 사용 독점을 막을 수 있어 효율적인 운영이 가능하지만 잦은 스위칭으로 오버헤드가 많이 발생한다.

### **2.2) 비선점형(Non-Preemptive) 스케줄링**

선점형과 반대로, 프로세스가 CPU를 점유하고 있다면 이를 빼앗을 수 없는 방식이다. 한 프로세스가 CPU를 점유했다면, I/O나 인터럽트가 발생 또는 프로세스가 종료될 때까지 다른 프로세스가 CPU를 점유하지 못하는 것이다.

필요한 스위칭만 일어나기 때문에 오버헤드가 상대적으로 적지만 프로세스 배치에 따라 효율성 차이가 많이 난다.

**스케줄러(Scheduler)**는 언제, 어떤 프로세스를 선택해서 CPU에서 실행시키는지 선택하는 모듈(Module)이다. 멀티프로그래밍의 목적이 CPU 효율 극대화이므로 적절한 스케줄링이 필요하다. 
 

## CPU 스케줄링

CPU 스케줄링은 프로세스 스케줄링의 하위 개념으로, CPU 시간의 할당에 초점을 맞춘 개념이다. 

기본적으로 프로세스는 CPU만 사용하는 단계(CPU burst)와 I/O 작업만 하는 단계(I/O burst)의 반복으로 구성된 사이클의 형태로 수행된다.

![image](https://github.com/user-attachments/assets/95be4af3-1062-4e6e-b8e9-f59aa68b055a)

CPU burst time의 분포에 따라 프로그램의 특성을 나타낼 수 있는데, 짧고 많은 CPU burst가 존재하는 프로그램을 I/O-bound Job, 길고 적은 CPU burst가 존재하는 프로그램을 CPU-bound Job이라고 부른다.
I/O-bound Job은 CPU를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 Job이다. 반면 CPU-bound Job은 계산 위주의 Job이다. 
그래프로 표현하면 아래와 같다.

![image](https://github.com/user-attachments/assets/4a5b70fa-3efd-40ee-8375-ee849b88ca8b)


이러한 여러 Job이 섞여있기 때문에 CPU 스케줄링이 필요하다. 
CPU Scheduler는 메모리에서 Ready 상태의 프로세스 중 어떤 프로세스를 CPU에 할당해줄지 선택한다. CPU 스케줄링으로 인해 변경되는 프로세스의 상태는 다음과 같다.

1. **Running → Waiting(Blocked)** : I/O 요청이나 자식의 종료를 위해 wait( ) 함수 호출한 경우
2. **Running → Ready** : 인터럽트가 발생한 경우
3. **Waiting → Ready** : I/O 작업이 끝난 경우
4. **Terminate**

여기서 1)과 4)는 Non-preemptive (비선점) 방식이고, 그 외의 모든 과정은 preemptive(선점) 방식이다.

Preemptive 방식은 **운영체제가 강제로 프로세스의 사용권을 통제하는 방식**이고, Non-preemptive 방식은 **프로세스가 스스로 다음 프로세스에게 자리를 넘겨주는 방식**이다.
Preemptive 스케줄링은 여러 프로세스가 데이터를 공유하고 있는 경우, 경쟁 상태(Race condition)의 문제점을 낳을 수 있다. 만약 한 프로세스가 데이터를 수정하고 있는 동안에 다른 프로세스의 수행을 위해 preempted 된다면, 다른 프로세스는 일관성이 없는 상태의 데이터를 읽게 된다.

## 스케줄링 기준

CPU 스케줄링 알고리즘은 여러 종류가 있는데, 각 알고리즘의 성능을 평가하는 기준(Performance measure, 성능 척도)이 있다.

1. 시스템 입장에서의 성능 척도 
- CPU 이용률 (CPU Utilization) : 전체 시간 중 CPU가 쉬지 않고 일한 시간
- 처리량 (Throughput) : 단위 시간당 수행 완료한 프로세스의 수

1. 프로그램 입장에서의 성능 척도 
- 소요 시간 (Turnaround Time) : 프로세스가 Ready queue에서 대기한 시간부터 작업을 완료하는데 걸리는 시간
- 대기 시간 (Waiting Time) : 프로세스가 Ready queue에서 대기한 시간
- 응답 시간 (Response Time) : 프로세스가 처음으로 CPU를 할당받기까지 걸린 시간

프로그램 입장에선 소요, 대기, 응답 시간이 모두 최소가 될수록 좋고, 시스템 입장에선 CPU 이용률과 처리량이 모두 최대가 될수록 좋다.

## 스케줄링 알고리즘

### **First-Come, First-Served(FCFS)**

**FCFS는 비선점형(Non-Preemptive) 스케줄링으로**, 먼저 온 프로세스가 먼저 CPU를 점유하는 방식이다.

| Process | Burst Time(msec) |
| --- | --- |
| P1 | 15 |
| P2 | 6 |
| P3 | 3 |

![image](https://github.com/user-attachments/assets/7242cfc1-c43d-4ee2-84ed-e640187c9ae5)

프로세스가 차례대로 **P1, P2, P3** 순서대로 들어왔다고 가정하고 평균 대기시간을 계산하면 아래와 같다.

**● Average Waiting Time:  (0+15+21) / 3= 12msec**

만약, 프로세스가 들어온 순서가 **P3, P2, P1이라면** 아래처럼 바뀔 것이다.

![image](https://github.com/user-attachments/assets/d142a2ab-ca84-4ff8-851b-9f43faea3c3f)

**● Average Waiting Time:  (0+3+9) / 3= 4 msec**

프로세스가 끝난 시간은 24 msec로 동일하지만, 평균 대기시간으로는 많은 차이를 보인다. 즉, 들어온 순서에 따라 효율성의 차이가 크게 생길 수 있다.

**P1, P2, P3** 순서로 들어온 것을 **Convoy Effect**라고 하는데, 이는 CPU 시간을 오래 사용하는 프로세스가 먼저 수행하는 동안 나머지 프로세스들은 그만큼 오래 기다리는 것을 일컫는다. 이는 FCFS의 단점 중 하나다.

### **Shortest-Job-First(SJF)**

**SJF**는 가장 짧게 수행되는 프로세스가 가장 먼저 수행되는 방식을 말한다.

**SJF**는 **선점형(Preemptive)과 비선점형(Non-Preemptive) 방식** 모두 가능하다.

| Process | Burst Time(msec) |
| --- | --- |
| P1 | 15 |
| P2 | 6 |
| P3 | 3 |

![image](https://github.com/user-attachments/assets/aa1fe91d-de78-46b9-86d7-9989e5ee6af7)


**● Average Waiting Time:  (0+3+9) / 3= 4 msec**

간단하게, FCFS방식에서 가장 CPU 사용시간이 낮은 시간 순서대로 들어온다고 생각하면 된다.

수학적으로 어떤 방식보다 평균 대기시간이 짧다고 할 수 있는데. 그렇다면 SJF가 가장 효율적인 스케줄링 방식일까? 사실 이 스케줄링 방법은 매우 **비현실적**이다.

현실적인 컴퓨터 환경에서는 프로세스의 CPU 점유 시간을 알 수 없을뿐더러 프로세스가 실행 중에는 많은 변수가 존재하기 때문에 CPU 점유 시간을 알려면 실제로 수행하여 측정하는 수밖에 없다. 하지만 이는 큰 오버헤드를 발생시키므로 잘 사용되지 않는다.

### **Priority**

**Priority** **스케줄링**은 우선순위가 높은 프로세스 먼저 선택되는 스케줄링 알고리즘이다.

**Priority 스케줄링**은 역시, **선점형(Preemptive)과 비선점형(Non-Preemptive) 방식** 모두 가능하다.

Priority가 낮을수록 우선순위가 높다고 가정하자.

| Process | Burst Time(msec) | Priority |
| --- | --- | --- |
| P1 | 10 | 3 |
| P2 | 1 | 1 |
| P3 | 2 | 4 |
| P4 | 1 | 2 |

![image](https://github.com/user-attachments/assets/3c8744b4-c732-4070-9c0e-5eec72efde45)


**● Average Waiting Time:  (0+1+2+12) / 4= 3.75 msec**

우선순위를 정하는 방법에는 크게 내부적인 요소와 외부적인 요소로 나뉜다.

- **Internal:** Time limit, Memory Requirement, I/O to CPU burst(I/O 작업은 길고, CPU 작업은 짧은 프로세스 순)
- **External:** Amount of funds being paid, Political Factors 등

Priority 스케줄링의 **문제점**은 **Starvation(기아)**이 있다. Starvation은 프로세스가 CPU 점유를 오랫동안 하지 못하는 현상을 일컫는데, 우선순위가 매우 낮은 프로세스가 대기하고 있다고 가정해보자. 이 프로세스는 아무리 오래 기다려도 CPU를 점유하지 못할 가능성이 매우 크다.

실제 컴퓨터 환경에서도 새로운 프로세스가 끊임없이 들어오고, 이러한 프로세스가 모두 우선순위가 높다면 이미 기다리고 있던 우선순위가 낮은 프로세스는 하염없이 기다리게 된다.

이를 해결하는 방법으로 **Aging**이 있는데 우선순위가 낮은 프로세스가 기다리는 동안 일정 시간이 지나면 우선순위를 일정량 높여주는 방식이다. 이렇게 한다면 우선순위가 낮더라도 시간이 지나면 우선순위가 높아지므로 수행될 가능성이 높아진다.

### **Round-Robin(RR)**

**Round-Robin(RR)은** 일정 시간을 정하여 각각의 프로세스가 이 시간 동안만 수행하고 다시 대기 상태로 돌아가는 방식을 말한다. **Round-Robin**은 기본적으로 선점형(Preemptive)이다. 일정 시간이 끝나면 다른 프로세스로 CPU를 넘겨주기 때문이다.

(Time Quantum = 3 msec)

| Process | Burst Time(msec) |
| --- | --- |
| P1 | 24 |
| P2 | 3 |
| P3 | 3 |

![image](https://github.com/user-attachments/assets/3ac16492-7a12-436d-93c6-966a6c28673e)

위에서 말한 일정 시간을 **Time Quantum(Time Slice)이라** 부른다. Time Quantum은 일반적으로 10~100 msec 사이의 범위를 갖는다. 위의 예는 Time Quantum이 3 msec이고 해당 단위별로 CPU를 점유하는 것을 볼 수 있다.

**● Average Waiting Time:  (0+3+6+6) / 3= 5 msec**

**RR**방식은 **Time Quantum**의 크기에 따라 매우 의존적인 것을 알 수 있다.

**Time Quantum** 크기를 무한에 가깝게 설정한다면 **FCFS**와 동일하게 동작하고. 반대로, 매우 작게 설정하면 스위칭 오버헤드가 매우 커서 비효율적이다. 즉 Time Quantum 값을 적당한 크기로 설정해줘야 한다.

### Reference

https://rebro.kr/175

https://cjwoov.tistory.com/58
