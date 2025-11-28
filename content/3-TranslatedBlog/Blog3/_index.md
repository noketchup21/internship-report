---
title : "Blog 3"
date :  "2025-09-09" 
weight : 1 
chapter : false
pre : " <b> 3. </b> "
---

## Seamlessly burst EDA jobs to AWS using Synopsys Cloud Hybrid solution

*This post was contributed by Varun Shah, Xingang Zhao (Synopsys), Dnyanesh Digraskar, Mayur Runwal (AWS)*

<div style="display: flex; align-items: flex-start; gap: 20px;">

<div style="flex: 1;">

In this post we describe how customers can burst their Synopsys workloads to AWS using [Synopsys Cloud Hybrid Solution](https://www.synopsys.com/blogs/chip-design/hybrid-cloud-chip-design-agility-efficiency.html). This simplifies the workflow by eliminating the need to manually move data between on-premises storage and the cloud. Data required by a job running on AWS is incrementally cached in the background and made available to the process. Similarly, when needed, selective data that’s written by a job running in the cloud can be pushed to on-premises in real time – keeping the on-premises storage up to date.

</div>

<img src="/images/Seamlessly-burst-EDA-jobs-to-AWS-using-Synopsys-Cloud-Hybrid-solution.png" alt="Figure 1" width="400" style="margin-top: -5px;"/>

</div>

<div style="margin-top: -40px;">

The semiconductor industry is experiencing explosive growth, driven by artificial intelligence (AI), high performance computing (HPC), and the proliferation of smart systems. Engineers are facing unprecedented complexity and an increasingly rapid pace of innovation. As chips become more powerful and intricate, design cycles grow longer, costs rise, and the risk of missing market windows increases. In this environment, time to market has become a critical differentiator.

</div>

Cloud-based infrastructure offers elasticity and flexibility to scale chip design operations and meet customer needs. AWS offers easy access to cloud compute resources which are optimized for EDA workloads. [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (Amazon EC2) provides access to the latest generation [processors](https://aws.amazon.com/ec2/instance-types/) in virtually unlimited capacity, deployable across the globe. Latest generation of x86 and ARM-based instances on AWS help realize maximum performance and let customers squeeze the most out of their EDA software licenses.

[Synopsys](https://www.synopsys.com/) is an AWS Partner delivering trusted and comprehensive silicon to systems design solutions for customers, from EDA to silicon IP and system verification and validation.

In this post we’ll demonstrate scale-testing a set of Synopsys EDA tools on AWS and describe performance, quality of results, and turnaround time.

### Synopsys Cloud Hybrid Solution: bursting EDA jobs to AWS

AWS makes it easy to setup cloud compute infrastructure with its large selection of hardware and services for [semiconductor and hi-tech](https://aws.amazon.com/manufacturing/semiconductor-hi-tech/) flows. Companies can match their compute needs with those of their time-critical workflows. At a high-level, the steps involved in bursting EDA workloads on AWS involve:

1. Identifying the design blocks/jobs that need to be run on the cloud
2. Transferring relevant data to the cloud
3. Installing EDA application binaries and licenses on the cloud
4. Running EDA jobs
5. Transferring the results back to on-premises for analysis/debug/reporting

Steps 1 & 2 above can be cumbersome as packaging the right set of files, source code, libraries, dependencies, scripts etc. can take up to several weeks of time. Synopsys Cloud Hybrid Solution provides a cloud-enabled mechanism to accomplish these tasks more easily.

### Architecture and Components

![Figure](/images/IMG-2025-09-23-16.23.34@2x.png)

*Figure 1: Architectural diagram of Synopsys Cloud Hybrid solution with AWS used for testing described in this blog*

Figure 1 shows the high-level architecture of the Synopsys Cloud Hybrid solution. The key architectural components include:

1. **On-premises storage:** These are the NFS mount points with design data that must be presented to the compute nodes on AWS. The hybrid solution works with any third-party or commercial ISV storage solutions.

2. **Scheduler:** The Hybrid solution works with any commercially available job schedulers like the ones in [AWS Parallel Computing Service (PCS)](https://aws.amazon.com/pcs/), [AWS ParallelCluster](https://aws.amazon.com/parallelcluster/), [AWS](https://aws.amazon.com/batch/) Batch, or IBM LSF, UGE, Slurm, etc. The architecture diagram illustrates the use of IBM LSF multi-cluster which integrates with [LSF resource connector](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=providers-configuring-amazon-web-services-lsf-resource-connector) for provisioning resources on AWS.

3. **Compute farms:**
    1. **On-premises:** This is the datacenter with a mix of several different types of compute servers.  
    2. **On AWS:** The Amazon EC2 instances used for performing the EDA simulations. For this testing, we used 16xlarge instances with 3.5GHz CPU, with 8GB memory per vCPU. A broad range of EC2 instance types could be used, depending on the application and semiconductor design under question.

4. **On Cloud NFS:** For EDA jobs which write intermediate data that isn’t required on-premises, an [Amazon FSx for NetApp ONTAP](https://aws.amazon.com/fsx/netapp-ontap/) filesystem was provisioned for use by compute resources on AWS.

5. **Synopsys Cloud Hybrid Solution:** Users install this binary on their Amazon EC2 instance and configure the data-sync to handle data movement between on-prem and AWS.

6. **Licensing:**
    1. **Licenses for EDA applications:** Existing EDA application licenses and license servers continue to serve licenses for jobs running on AWS. Any additional license needs can be served by Synopsys [FlexEDA](https://www.synopsys.com/blogs/chip-design/what-is-flexeda.html) and Pay-Per-Use metered licensing.  
    2. **License for Hybrid solution:** This is a separate application that needs to be purchased by the users from Synopsys. The licensing is served from Synopsys managed network license servers.

### Setting up the Synopsys Cloud Hybrid Solution

The setup includes 3 main components:

1. **Hybrid Cloud data-sync**: This entails installing the Hybrid solution on a recommended instance type on AWS, configure networking to allow traffic across on-premises and AWS resources for licensing (of Hybrid Cloud solution), data storage and distributed processing, identifying NFS storage mounts on-prem that require mapping and starting the Hybrid solution to establish the data-sync mapping.
2. **Network Connectivity**: Dedicated network connections like [AWS DirectConnect](https://aws.amazon.com/directconnect/) provide higher bandwidth, lower latency which makes it ideal for handling workloads with large data transfers. Alternatively, IPsec Virtual Private Network (VPN) tunnel can be used with AWS but offers less speed and reliability compared to dedicated network connections.
3. **Scheduler setup**: This is specific to every scheduler. For example, in the case of IBM LSF, this involves deploying LSF multi-cluster, defining participating clusters, configuring queues and verifying that clusters on AWS can be dynamically provisioned as needed.

### General information about the platform

With , selective data that is written by a job running on cloud, can be written back to on-premises in real time, thereby keeping the on-premises storage up to date. Note that data write-back incurs data egress charges from AWS. Temporary output data from running jobs that’s not required on-prem or large persistent output data can be directed to an NFS on-cloud. If necessary, this data can be scripted to write-back after job completion.

The job scheduler should be provisioned by the customer. It then finds an appropriate compute resource, on-premises or on AWS, and the Hybrid Solution handles the data movement necessary. Synopsys Cloud Hybrid Solution has ability to configure the scheduler to automatically exhaust on-premises compute capacity first and then schedule jobs on-cloud compute nodes, or to run all jobs on cloud compute nodes depending on the application being run and size/frequency of data being shared between different workers of the application.

### Scale-testing Synopsys Hybrid Solution on AWS

EDA jobs can be data intensive both in terms of input and output. The latency of the network and the amount of data moving back and forth can impact the performance of EDA jobs. To understand the boundaries of the Synopsys Hybrid Solution, we used six of Synopsys’ flagship applications which are essential for every semiconductor chip design process. These are:

- [PrimeLib](https://www.synopsys.com/implementation-and-signoff/signoff/primelib.html) – a library characterization and validation application
- [Synopsys VCS](https://www.synopsys.com/verification/simulation/vcs.html) – Simulator for verifying semiconductor designs
- [PrimeSim SPICE](https://www.synopsys.com/implementation-and-signoff/ams-simulation/primesim-spice.html) – GPU-accelerated SPICE Simulator for Analog, RF, and - Mixed-signal Design
- [Synopsys PrimeWave](https://www.synopsys.com/implementation-and-signoff/ams-simulation/primewave.html) – application for simulation setup and analysis of analog, RF, mixed-signal design, custom-digital and memory designs
- [PrimeTime](https://www.synopsys.com/implementation-and-signoff/signoff/primetime.html) – static timing analysis application with fast, memory-efficient scalar and multicore computing
- [Synopsys DSO.ai](https://www.synopsys.com/ai/ai-powered-eda/dso-ai.html) – an AI-powered design space optimization application

All these EDA applications have different profiles in terms of I/O patterns, amount of data generated (size and volume of files), and the amount and frequency of communication that happens between different workers of a job. Each of these applications were executed using the Synopsys Cloud Hybrid Solution with standard designs and testcases. We prioritized jobs that require high IOPs when selecting the testcases for the benchmarking exercise.

We monitored several metrics and compared them between tests performed on Synopsys Cloud Solution on AWS and comparable on-premises infrastructure:

1. **Performance**: Runtime performance is a critical metric as it directly translates to time to market.
2. **Quality of Results** (QoR): QoR is another critical metric that cannot be compromised on.
The applications analyze the results in terms of coverage, passing tests and regressions and the output their interpretation of the overall quality of results. For the applications tested, we expect to see same or similar QoR results between AWS and on-premises tests.
3. **Setup time**: If performance and QoR are reasonably on-par, then what makes Synopsys Cloud Hybrid Solution worthwhile is the time that can be saved in moving relevant data to the cloud to use AWS compute infrastructure. While it’s hard to measure this on-premises and differs greatly from one EDA flow to another, we tried to estimate this.

### Results
#### Performance

![Figure](/images/IMG-2025-09-23-16.26.12@2x.png)
*Table 1: Performance of Synopsys applications run on Hybrid Solution with AWS vs on-premises*

We ran this baseline of tests either on-premises or on AWS depending on resource availability on premises. Table 1 shows that the overall performance of all EDA flows tested using Synopsys Cloud Hybrid Solution was comparable to – or in some cases, better than – the baseline. In the case of Hybrid Setup, the runtime includes time taken to write final output data back to on-premises storage through the Hybrid Solution. This impacts the overall performance slightly when compared to a baseline run natively on cloud like in the case of PrimeLib and VCS. The data also shows that performance was better than a baseline run on-premises for PrimeTime and PrimeSim. This is due to the availability of faster CPUs on AWS.

Through understanding IO patterns (size, frequency) of different EDA applications, we identified some best practices for setting up these applications to best use the Hybrid Solution.

#### Quality of Results (QoR)

As expected, there was no degradation in quality of results, PPA or coverage achieved when using the Hybrid Solution. For EDA applications like VCS, PrimeSim, results matched exactly with the runs on-premises. For other EDA applications like DSO.ai, the reports, PPA and QoR is comparable.

#### Setup Time:

Synopsys Hybrid Cloud saves up to several weeks of setup time per project by automating the manual data movement and verification of design blocks. For example, from our own internal testing of an EDA application’s QA regressions, we know that ~4 weeks of manual effort was saved because Hybrid Solution eliminated the need to lift and shift EDA workloads.

Depending on the workflows, Synopsys can help in best practice recommendations on a cloud-native mode or a burst mode with Synopsys Cloud Hybrid Solution. With the true burst mode, data is written to on-cloud NFS, and then selective data is synced back to on-premises after the job completion. In this way, data egress and performance impacts are minimized. Burst mode adds huge value by incrementally moving input data as needed to the cloud for running the jobs through Hybrid Solution.

### Conclusion

EDA workloads demand immense computational power and seamless data access. The sheer volume of design data, coupled with the iterative and highly interdependent nature of EDA tasks, means that constant data movement between on-premises storage and cloud compute can become a slow and inefficient process.

[Synopsys Cloud Hybrid Solution](https://www.synopsys.com/cloud.html) solves this problem by providing a seamless way to burst EDA jobs from on-premises to the cloud with real-time two-way data synchronization. The product was stress-tested with six of Synospys’ flagship EDA applications. We found that performance of applications in Hybrid mode was comparable to performance of an on-premises or cloud-native run all while maintaining the same Quality of Results. Data movement was invisibly handled by Synopsys Cloud Hybrid Solution which saved up to weeks of setup time.

---

### Varun Shah
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/IMG-2025-09-23-16.35.10@2x.png" alt="Varun Shah" width="150"/>

<div>
Varun Shah is on the product management team for Synopsys Cloud, responsible for technology roadmap, cloud enablement of EDA software and voice-of-customer analysis. Varun holds a master's degree in electrical engineering from the University of Missouri-Rolla and is a certified product management professional from the Kellogg School of Management.
</div>
</div>

---

### Dnyanesh Digraskar
<div style="display: flex; align-items: center; gap: 15px;">
  <img src="/images/dnyanesh.png" alt="Dnyanesh Digraskar" width="150"/>
  <div>
Dnyanesh Digraskar is a Principal HPC Partner Solutions Architect at AWS. He leads the HPC implementation strategy with AWS ISV partners to help them build scalable well-architected solutions. He has more than fifteen years of expertise in the areas of CFD, CAE, Numerical Simulations, and HPC. Dnyanesh holds a Master’s degree in Mechanical Engineering from University of Massachusetts, Amherst.
  </div>
</div>

---

### Mayur Runwal
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/IMG-2025-09-23-16.35.44@2x.png" alt="Mayur Runwal" width="150"/>

<div>
Mayur Runwal is a Senior Solutions Architect at AWS specializing in Electronic Design Automation (EDA). He architects semiconductor design and verification workflows for AWS customers. Before joining AWS, he led IT infrastructure teams at semiconductor companies for 10 years, where he designed and implemented virtual desktop solutions. His expertise includes high-performance computing, cloud architecture, and enterprise IT solutions.
</div>
</div>

---

### Xingang Zhao
<div style="display: flex; align-items: center; gap: 15px;">

<img src="/images/IMG-2025-09-23-16.35.23@2x.png" alt="Xingang Zhao" width="150"/>

<div>
Xingang Zhao is a Technical Product Manager for Synopsys Cloud. He's responsible for the technical assessment and integration of emerging cloud services and tools on public cloud platforms to boost the performance and cost-effectiveness of EDA workloads. Xingang holds a BS in electrical engineering from Zhejiang University and is a certified product management professional from the Kellogg School of Management.
</div>
</div>