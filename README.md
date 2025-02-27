[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Zou Muyang
### Student Id: 21074119
### Email: mzouad@connect.ust.hk (zoumygeekinpink@163.com)

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    >I am using the measurement tool Phoronix Test Suite.\
    > \
    >The command to test CPU performance is:  \
    >***phoronix-test-suite run pts/compress-7zip*** \
    > This command test the system's performance of compressing and decompressing files using 7-Zip. I didn't set any additional parameters. I choose the result value in MIPS (Million Instructions Per Second) in Compression task to measure CPU performance.\
    > \
    > The command to test memory performance is: \
    > ***phoronix-test-suite run pts/ramspeed*** \
    > This command runs the RAM Speed benchmark to evaluate the performance of the computer system's memory. I set the parameters to Copy and Integer, so it runs the Integer type memory copy operation test. The command returns a value representing the memory copy speed.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |      4083 MIPS           |       11539.24 MB/s            |
    | `t2.medium`  |           10156 MIPS      |           20025.72 MB/s         |
    | `c5d.large` |        7449 MIPS         |              13774.53 MB/s      |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.
    > Compression, Copy
## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |      3.64 Gbits/sec (3727.26 Mbps)          |      0.259 ms    |
    | `m5.large` - `m5.large`   |       4.95 Gbits/sec (5068.8 Mbps)        |    0.233 ms      |
    | `c5n.large` - `c5n.large` |        4.96 Gbits/sec (5079.04 Mbps)       |      0.161 ms    |
    | `t3.medium` - `c5n.large` |       2.20 Gbits/sec (2252.8 Mbps)         |     0.784 ms     |
    | `m5.large` - `c5n.large`  |       2.45 Gbits/ sec (2508.8 Mbps)         |       0.769 ms   |
    | `m5.large` - `t3.medium`  |         4.35 Gbits/sec (4454.4 Mbps)      |      0.176 ms    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |        32.2 Mbits/sec        |     61.1 ms     |
    | N. Virginia - N. Virginia |       4.96 Gbits/sec         |     0.208 ms     |
    | Oregon - Oregon           |         4.96 Gbits/sec       |       0.168 ms   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
