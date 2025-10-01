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
