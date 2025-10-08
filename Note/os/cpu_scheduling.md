### CPU scheduling

Switching between two or more processes are the lower level mechanism that OS
applies. However, Scheduling is higher level policies sometime calls **discipline**
developed by various hardworking and smart people.

There are different policies so we need some assumption and matrices to compare
policies.

1. Each job runs for the same amount of time.
2. All jobs arrive at the same time.
3. Once started, each job runs to completion.
4. All job use CPU only
5. The run time of each job is known.

Collectively we assume a workload of a process.

> **Turn around Time**: The turn around time of a job is define as time take to
complete job minus arrival time of job.
*T<sub>turnaround</sub> = T<sub>completion</sub> - T<sub>arrival</sub>*.

Since we have assume arrive time of every process is same, then we can say
*T<sub>arrival</sub> = 0 then T<sub>turnaround</sub>=T<sub>completion</sub>*.

Turn around time is a **performance** metric. Another metric of interest is 
**fairness** as measured. Performance and Fairness are two odds in scheduling.
Many wants to optimize performance at cost of running few processes thus decreasing
fairness.

- **First In First Out (FIFO)**: The most basic algorithm we can implement is 
FIFO or sometime called First Come First Serve (FCFS). It is an easy implement.
If three different processes A, B and C are almost arrive at the same time then
from our assumptions it is a quite effective algorithm. Assuming each job run
for 10s.\
![FIFO](resource/os_image5.png)\
Average Turnaround time will be <sup>(10+20+30)</sup>&frasl;<sub>3</sub>=20.\
Let's drop the first assumption "*Each job runs for the same amount of time*".
This time A runs for 100s and B and C run for 10s\
![FIFO](resource/os_image6.png)\
Average Turnaround time will be <sup>(100+110+120)</sup>&frasl;<sub>3</sub> = 110.
This is called `**convoy effect**` where relatively light resource consumers get
queued behind heavy resource consumers.

- **Short Job First**: This is another method of cpu scheduling which avoid
**convoy effect**. The name describe the policy itself. It runs the shortest
job first and go to next shortest and so on.\
![SJF](resource/os_image7.png)\
Average Turnaround time will be <sup>(10+20+120)</sup>&frasl;<sub>3</sub> = 50.
Given our assumption "*All job will arrive at same time*" SJF is indeed an optimal
algorithm. But our assumption is unrealistic so, let's drop that assumption now
that job can arrive any time.\
Let's assume A arrives at first which have to run 100s the job B and C arrives
which came 10s after the A arrives and have to run for 10s each.
![SJF](resource/os_image8.png)\
And we are back to same the problem because A arrives at first so it is force to
run until it has completed and only after that B and C will get their turn to 
execute.\
Turnaround time will be <sup>(100+(110-10)+(120-10))</sup>&frasl;<sub>3</sub>
=103.33 .

- **Shortest Time-to-Completion First**: To address above issue we have to drop
another assumption "*Once started, each job should run to completion*". After
new jobs arrive STFC determine which job has shortest remaining time to complete
and switch to it.\
![STFC](resource/os_image9.png)\
In above image, A arrives at first that has 100s completion time then CPU start
executing it. After 10s new two jobs arrives B and C which has only 10s 
completion time. Since, B and C has less completion time scheduler switch to
B or C.\
Turn around time will be <sup>(120+(20-10)+(30-10))</sup>&frasl;<sub>3</sub> 
= 50.

User demands interactive performance from the system thus, new metric is defined
**Response Time**. We define response time as time from when job arrives in 
a system and to the first time it is scheduled.\
T<sub>response</sub> = T<sub>first turn</sub> - T<sub>arrives</sub>\
STFC and related policies are not best for the responsive system.

- **Round Robin**: To make the system more responsive new scheduling policy is
introduced called **Round Robin(RR)**. The idea is simple instead of running
job to completion it just run each job for a certain **time slice**. It repeatedly
does so until all jobs finished.\
Assume job A, B and C arrives at the system at the same time each job require
5s to complete. For RR time-slice of 1s would cycle through the job quickly.\
The response time for RR is <sup>0+1+2</sup>&frasl;<sub>3</sub> = 1.\
The response time for STFC is <sup>0+5+10</sup>&frasl;<sub>3</sub> = 5.\
As we can see time-slice is critical to RR. The lower the time-slice the more
system became responsive in RR. However, making time-slice too small is 
problematic because we have to consider the cost of context switching.\
![RR](resource/os_image10.png)\
Generally, any policy that are fair (like RR) i.e. evenly divides the CPU among
processes on a small timescale will perform poorly on turnaround time metrics.

- Incorporating I/O: First of all we have to drop our assumption *All job use 
cpu only*. We need program that takes input and give output. When currently 
running job request I/O clearly CPU is not utilized at that blocked state thus
scheduler have to assign another job at that time. Once, I/O complete OS return
the process from block state to ready state and scheduler can decide to weather
run that process immediately or not.\
Let's assume we have two jobs A and B each needs 50ms of CPU. However, A runs 10ms
and issue I/O request and I/O takes 10 milliseconds.\
A common approach is to take 10ms subjob of A as entirely different task. Then
schedular choose either to run 10ms A or 50 ms B. Assuming we are using STFC
schedular we choose 10ms A to run first after subjob of A is completed B will
run, after I/O request completed a new subjob A is submitted.\
![IO](resource/os_image11.png)\
The main idea behind this approach is make CPU busy while other processes are
waiting for I/O.

Another Big hurdle over developing scheduler is: we don't know the length of jobs.
Until now, we are assuming *The run time each job is known* but this is unrealistic
assumption. Scheduling method line STFC, SJF are build upon this assumption.

### The Multi-level Feedback Queue

The Multi-level Feedback Queue (MLFQ) is firstly introduced by **Corbato et al.**
in 1962 AD in a system known as Compatible Time-Sharing System `(CTSS)`. The 
problem MLFQ tries to solve is optimize Turn around time without prior knowledge 
of job length. Second, MLFQ would like to make system responsive by minimizing
Response time.

MLFQ has different queue which have different `priority level`. A job with higher
priority will run more often. Jobs with same priority will use `Round Robin`
scheduling.

- Rule 1: If priority(A)>priority(B) then A runs B doesn't.
- Rule 2: If priority(A)=priority(B) then A and B run in RR.

MLFQ varies the job priority based on its behavior. If a jobs repeatedly waiting
for input, MLFQ put its priority high. If job uses CPU intensively for a long 
period of time, MLFQ lower its priority. In this way MLFQ learns about processes
behavior and predict its future behavior.

#### How to change priority

When job is firstly introduced, it is placed at higher priority then change its
priority over the lifetime.

- Rule 3: When job enters the system, it is placed at highest priority.
- Rule 4: If job uses entire time slice while running, it priority is reduced.
- Rule 5: If job gives up the CPU before time slice, it stays at same priority 
level.

![MLFQ](resource/os_image12.png)\
As we can see, A enters at highest priority and gradually it's priority decreased.

What happened when a short running job arrives? Let's say B. Now there are two 
jobs long running A and short running B.

![MLFQ](resource/os_image13.png)\
It doesn't know weather jobs are long running or short running. It assume a job
is short running at first, it run and quickly finished; if it isn't short job then
it reduce priority slowly and proving itself a long running job.

#### What about I/O?
When an interactive job does a lot of I/O then it will give up CPU before time
slice. In this case we don't reduce job's priority according to **Rule 5**.\
Let's say B is an interactive job which need CPU for very short amount of time
before performing I/O which is competing against long running Job A.

![MLFQ](resource/os_image14.png)\
B is staying at the top because it gives up cpu before time slice.

At this point, MLFQ doing fairly good but there is problem called **Starvation**.
When there are "too many" interactive jobs in the system, they will consume all
the CPU in return low priority job won't get any chance to run.

![MLFQ](resource/os_image15.png)\

Secondly, user can rewrite the program to **game the scheduler**. Gaming a 
scheduler is a technique in which user tricked the scheduler to give more 
resource to their program than fair resource distribution. In this case,
we can do that by making I/O operation before time slice which we don't care 
about in result our program stays at top priority and get more CPU time.

