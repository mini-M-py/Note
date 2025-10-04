### CPU scheduling

Switching between two or more processes are the lower level mechaninsm that OS
applies. However, Scheduling is higher level policies sometime calls **discipline**
developed by various hardworking and smart people.

There are different policies so we need some assumtion and metrices to comapre
policies.

1. Each job runs for the same amount of time.
2. All jobs arrive at the same time.
3. Once started, each job runs to completion.
4. All job use CPU only
5. The run time of each job is known.

Collectively we assume a workload of a process.

> **Turnaround Time**: The turn around time of a job is define as time take to
complete job minus arrival time of job.
*T<sub>turnaround</sub> = T<sub>completion</sub> - T<sub>arrival</sub>*.

Since we have assume arrive time of every procees is same then we can say
*T<sub>arrival</sub> = 0 then T<sub>turnaround</sub>=T<sub>completion</sub>*.

Turnarond time is a **performance** matric. Another metric of interest is 
**fairness** as measured. Performance and Faireness are two odds in scheduling.
Many wants to optimize performance at cost of running few processes thus decreasing
fairness.

- **First In First Out (FIFO)**: The most basic algorithm we can implement is 
FIFO or sometime called First Come First Serve (FCFS).  It is easy implement.
If three different processes A, B and C are almost arrive at the same time then
from our assumtions it is a quite effective algorithm. Asssumeing each job run
for 10s.

![FIFO](resource/os_image5.png)

Average Turnaround time will be <sup>(10+20+30)</sup>&frasl;<sub>3</sub>=20.

Let's drop the first assumtion "*Each job runs for the same amount of time*".
This time A runs for 100s and B and C run for 10s

![FIFO](resource/os_image6.png)

Average Turnaround time will be <sup>(100+110+120)</sup>&frasl;<sub>3</sub> = 110.
This is called **convoy effect** where relatively light resource consumers get
queued behind heavy resource consumers.


