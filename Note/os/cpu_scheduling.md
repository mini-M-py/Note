### CPU scheduling

Switching between two or more processes is the lower-level mechanism that the OS
applies. However, Scheduling is a higher-level policy sometimes called **discipline**
developed by various hardworking and smart people.

There are different policies, so we need some assumptions and matrices to compare
policies.

1. Each job runs for the same amount of time.
2. All jobs arrive at the same time.
3. Once started, each job runs to completion.
4. All jobs use the CPU only
5. The run time of each job is known.

Collectively, we assume a workload for a process.

> **Turnaround Time**: The turnaround time of a job is defined as the time taken to
complete the job minus the arrival time of the job.
*T<sub>turnaround</sub> = T<sub>completion</sub> - T<sub>arrival</sub>*.

Since we have assumed the arrival time of every process is the same, we can say
*T<sub>arrival</sub> = 0 then T<sub>turnaround</sub>=T<sub>completion</sub>*.

Turn-around time is a **performance** metric. Another metric of interest is 
**fairness** as measured. Performance and Fairness are two odds in scheduling.
Many want to optimize performance at the cost of running a few processes, thus decreasing
fairness.

- **First In First Out (FIFO)**: The most basic algorithm we can implement is 
FIFO, or sometimes called First Come First Serve (FCFS). It is an easy implementation.
If three different processes A, B, and C are almost at the same time, then
from our assumptions, it is quite an effective algorithm. Assuming each job runs
for 10s.\
![FIFO](resource/os_image5.png)\
Average Turnaround time will be <sup>(10+20+30)</sup>&frasl;<sub>3</sub>=20.\
Let's drop the first assumption, "*Each job runs for the same amount of time*".
This time A runs for 100s and B and C run for 10s\
![FIFO](resource/os_image6.png)\
Average Turnaround time will be <sup>(100+110+120)</sup>&frasl;<sub>3</sub> = 110.
This is called `**convoy effect**`, where relatively light resource consumers get
queued behind heavy resource consumers.

- **Short Job First**: This is another method of CPU scheduling, which avoids
**convoy effect**. The name describes the policy itself. It runs the shortest
job first and goes to the next shortest and so on.\
![SJF](resource/os_image7.png)\
Average Turnaround time will be <sup>(10+20+120)</sup>&frasl;<sub>3</sub> = 50.
Given our assumption "*All jobs will arrive at the same time*", SJF is indeed an optimal
algorithm. But our assumption is unrealistic, so let's drop that assumption now
that the job can arrive any time.\
Let's assume A arrives first, which has to run 100s of jobs. B and C arrive,
 which came 10s after A arrives, and have to run for 10s each.
![SJF](resource/os_image8.png)\
And we are back to the same problem because A arrives first, so it is forced to
run until it has completed, and only after that, B and C will get their turn to 
execute.\
Turnaround time will be <sup>(100+(110-10)+(120-10))</sup>&frasl;<sub>3</sub>
=103.33.

- **Shortest Time-to-Completion First**: To address the above issue, we have to drop
another assumption, "*Once started, each job should run to completion*". After
new jobs arrive, STFC determines which job has the shortest remaining time to complete
and switches to it.\
![STFC](resource/os_image9.png)\
In the above image, A arrives first, which has a 100s completion time, then  the CPU starts
executing it. After 10s, two new jobs arrive, B and C, which have only 10s 
completion time. Since B and C have less completion time scheduler switches to
B or C.. \
Turn around time will be <sup>(120+(20-10)+(30-10))</sup>&frasl;<sub>3</sub> 
= 50.

User demands interactive performance from the system; thus, a new metric is defined
**Response Time**. We define response time as the time from when a job arrives in 
a system to the first time it is scheduled.\
T<sub>response</sub> = T<sub>first turn</sub> - T<sub>arrives</sub>\
STFC and related policies are not the best for the responsive system.

- **Round Robin**: To make the system more responsive new scheduling policy is
introduced called **Round Robin(RR)**. The idea is simple: instead of running
a job to completion, it just runs each job for a certain **time slice**. It repeatedly
does so until all jobs are finished.\
Assume jobs A, B, and C arrive at the system at the same time; each job requires
5s to complete. For RR time slice of 1s would cycle through the job quickly.\
The response time for RR is <sup>0+1+2</sup>&frasl;<sub>3</sub> = 1.\
The response time for STFC is <sup>0+5+10</sup>&frasl;<sub>3</sub> = 5.\
As we can see time slice is critical to RR. The lower the time slice, the more
the system becomes in RR. However, making the time slice too small is 
problematic because we have to consider the cost of context switching.\
![RR](resource/os_image10.png)\
Generally, any fair policy (like RR), i.e., evenly divides the CPU among
processes on a small timescale, will perform poorly on turnaround time metrics.

- Incorporating I/O: First of all, we have to drop our assumption *All jobs use 
CPU only*. We need a program that takes input and gives output. When the  currently 
running job request I/O is clearly CPU is not utilized in that blocked state, thus
the scheduler has to assign another job at that time. Once I/O is complete OS returns
the process from the block state to the ready state, and the scheduler can decide whether to 
run that process immediately or not.\
Let's assume we have two jobs, A and B, each needs 50ms of CPU. However, A runs 10ms
and issue I/O request and I/O takes 10 milliseconds.\
A common approach is to take a 10ms subjob of A as an entirely different task. Then
the scheduler chooses either to run 10ms A or 50ms B. Assuming we are using the STFC
scheduler, we choose 10ms A to run first after the subjob of A is completed, and B will
run. After the I/O request is completed, a new subjob A is submitted.\
![IO](resource/os_image11.png)\
The main idea behind this approach is to make the CPU busy while other processes are
waiting for I/O.

Another Big hurdle to developing a scheduler is: we don't know the length of jobs.
Until now, we have been assuming *The run time of each job is known*, but this is an unrealistic
assumption. Scheduling methods like STFC, SJF are built upon this assumption.

### The Multi-level Feedback Queue

The Multi-level Feedback Queue (MLFQ) was first introduced by **Corbato et al.**
In 1962 AD, in a system known as the Compatible Time-Sharing System `(CTSS)`. The 
problem MLFQ tries to solve is to optimize turnaround time without prior knowledge 
of job length. Second, MLFQ would like to make the system responsive by minimizing
Response time.

MLFQ has different queues that have different `priority levels`. A job with higher
priority will run more often. Jobs with the same priority will use `Round Robin`
scheduling.

- Rule 1: If priority(A)>priority(B) then A runs B doesn't.
- Rule 2: If priority(A)=priority(B) then A and B run in RR.

MLFQ varies the job priority based on its behavior. If a job repeatedly waits
for input, MLFQ puts its priority high. If a job uses the CPU intensively for a long 
period of time, MLFQ lowers its priority. In this way, MLFQ learns about process
behavior and predicts its future behavior.

#### How to change priority

When a job is first introduced, it is placed at a higher priority than changing its
priority over the lifetime.

- Rule 3: When a job enters the system, it is placed at the highest priority.
- Rule 4: If a job uses the entire time slice while running, its priority is reduced.
- Rule 5: If a job gives up the CPU before its time slice, it stays at the same priority 
level.

![MLFQ](resource/os_image12.png)\
As we can see, A enters at the highest priority and gradually its priority decreases.

What happens when a short-running job arrives? Let's say B. Now there are two 
Jobs are long-running A and short-running B.

![MLFQ](resource/os_image13.png)\
It doesn't know whether jobs are long-running or short-running. It assumes a job
It is short running at first, it runs and quickly finishes; if it isn't a short job, then
It reduces priority slowly and proves itself to be a long-running job.

#### What about I/O?
When an interactive job does a lot of I/O, it will give up the CPU before the time
slice. In this case, we don't reduce the job's priority according to **Rule 5**.\
Let's say B is an interactive job that needs CPU for a very short amount of time
before performing I/O, which is competing against long-running Job A.

![MLFQ](resource/os_image14.png)\
B is staying at the top because it gives up cpu before the time slice.

At this point, MLFQ is doing fairly good, but there is a problem called **Starvation**.
When there are "too many" interactive jobs in the system, they will consume all
the CPU in return  low-priority jobs won't get any chance to run.

![MLFQ](resource/os_image15.png)\

Secondly, the user can rewrite the program to **game the scheduler**. Gaming a 
Scheduler is a technique in which the user tricks the scheduler to give more 
resource to their program than fair resource distribution. In this case,
We can do that by making an I/O operation before the time slice, which we don't care about 
As in result, our program stays at the top priority and gets more CPU time.

