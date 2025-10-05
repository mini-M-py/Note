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
for 10s.\
![FIFO](resource/os_image5.png)\
Average Turnaround time will be <sup>(10+20+30)</sup>&frasl;<sub>3</sub>=20.\
Let's drop the first assumtion "*Each job runs for the same amount of time*".
This time A runs for 100s and B and C run for 10s\
![FIFO](resource/os_image6.png)\
Average Turnaround time will be <sup>(100+110+120)</sup>&frasl;<sub>3</sub> = 110.
This is called **convoy effect** where relatively light resource consumers get
queued behind heavy resource consumers.

- **Short Job First**: This is the another method of cpu scheduling which avoid
**convoy effect**. The name describe the policy itself. It runs the shortest
job first and go to next shortest and so on.\
![SJF](resource/os_image7.png)\
Average Turnaround time will be <sup>(10+20+120)</sup>&frasl;<sub>3</sub> = 50.
Given our assumtion "*All job will arrive at same time*" SJF is indeed a optimal
algorithm. But our assumtion is unrealistic so, let's drop that assumtion now
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
another assumtion "*Once started, each job should run to completion*". After
new jobs arrive STFC determine which job has shortest remaining time to complete
and switch to it.\
![STFC](resource/os_image9.png)\
In above image, A arrives at first that has 100s completion time then CPU start
executing it. After 10s new two jobs arrives B and C which has only 10s 
completion time. Since, B and C has less completion time schedular switch to
B or C.\
Turnaround time will be <sup>(120+(20-10)+(30-10))</sup>&frasl;<sub>3</sub> 
= 50.

User demands interactive performance from the system thus, new matric is defined
**Response Time**. We define resoponse time as time from when job arrives in 
a system and to the first time it is scheduled.\
T<sub>response</sub> = T<sub>first turn</sub> - T<sub>arrives</sub>\
STFC and related policies are not best for the responsive system.











