<!--

author:   Scott Feister

email:    scott.feister@csuci.edu

version:  0.0.1

language: en

narrator: US English Female

comment:  GPU Lab for COMP 262: Computer
          Organization and Architecture
          COMP 262, Fall 2023.

-->

# GPU Laboratory

In this lab, we will design a simple data encryption algorithm and implement it (and assess its benchmarks) on both a GPU and CPU.

## Learning Outcomes

Upon completing this laboratory, students will:

* Examine separation of GPU memory caches and CPU memory caches (So data transfer across the bus is needed at some step even if the CPU has already been working on the data)
* Examine differences in generality CPU instruction sets and GPU instruction sets
* Demonstrate the massive parallelism of a GPU through kernel-level computer programming
* Explore situations where GPUs are faster, and CPUs are faster, and do fine-grained benchmark to show how memory transfer and GPU clock speed impacts these outcomes
* Showcase one application of GPUs, encryption of data, using CUDA programming


## Pre-Work (Three Weeks in Advance)
You will complete the following pre-work in class, three weeks in advance of the lab day.

### Apply for a NERSC Account (15 minutes)

Later this semester, I am going to have everyone in the class access a supercomputer to complete labs relating to parallel processors and GPU computing. I have an award of supercomputing time granted to me from a [government-funded national supercomputer center](https://www.nersc.gov/). This center, called NERSC, is located in San Francisco. We will likely be accessing limited numbers of computing nodes on the [Perlmutter supercomputer](https://www.nersc.gov/systems/perlmutter/). You can [read about the architecture here](https://docs.nersc.gov/systems/perlmutter/architecture/).

Note from NERSC staff, before proceeding:

> Your account will undergo user vetting, in accordance with NERSC policies, to verify your identity. Under some circumstances, there could be a delay of up to a week while this vetting takes place.

NERSC representatives have assured me this user vetting is lighter than a typical background check, and importantly, does not involve investigation of immigration status. Please reach out to me directly if you'd like more details before proceeding, and I will find out more.

#### Step-by-Step: Apply for a NERSC Account
Here's how students enrolled in COMP 262 at CSUCI can sign up for an account at NERSC:

1. Navigate to [NERSC Add User](https://iris.nersc.gov/add-user)
2. Select "I need a new NERSC account"
3. Click ORCID n/a
4.  Pick a username that is your first initial + last name. (If that's taken, add a number at the end -- and if your name is too long, truncate this. Example: If your name is Jane Doe, choose "jdoe" or "jdoe5".)
5.  Search by PI Name, type "feister", and select m4347 (coa)
6.  Fill out your name and citizenship.
7.  For organization, type "California State University Channel Islands (CSUCI)"
8.  For Department, type "Computer Science"
9.  For Work role, select "UNDERGRAD"
10. For email, use your official CSUCI email.
11. For Work Phone, add your real phone number., e.g. your cell phone or home number.
12. For comments, note "I am an undergraduate in Dr Scott Feister's COMP 262 Spring 2023 class at CSUCI."
13. Confirm you aren't a robot.
14. Click "Ok" to submit your form.

After you're done, there will be a security vetting step that may take a couple days. Then I'll approve you on my end, and then you're in.

#### Submit: A Screenshot of Application (Due During Class Period)
Submit a screenshot of your confirmation email showing you have signed up for an account at NERSC.

## Pre-Work (Two Weeks in Advance)
You will complete the following pre-work in class, two weeks in advance of the lab day.

This week's pre-work requires that you already completed last week's pre-work. Once you receive an email saying your account has been created, you can continue with this week's pre-work.

### Activate Your NERSC Account (5 minutes)
Several days after your initial application for a NERSC account (last week's pre-work), you will receive an email from NERSC saying that your account has been approved, and with instructions to activate your new account. Follow the link in your email to activate your NERSC account.

**Note: Make Sure to Write Down your NERSC Password**
The password reset process takes about an hour, if you do forget, then reset your password, wait an hour, then try logging in again.

### Enable Multi-Factor Authentication for Your NERSC Account (10 minutes)

The tools we will be using at NERSC requires you user account to have multi-factor authentication (MFA) enabled. In this section of pre-work, you'll enable and test multi-factor authentication. You'll need your mobile phone for this pre-work, as it involves installing an app.

#### Step-by-Step: Enable Multi-Factor Authentication (MFA)
You'll install an authenticator app on your phone, and use that app to get a unique "one-time password" (OTP), or "token", each time you login to NERSC. This token is in addition to your regular NERSC password.

1. Open a new browser tab and follow the [official NERSC instructions to set up MFA](https://docs.nersc.gov/connect/mfa/).
2. When you get to the section titled "Testing Your New Token", save a screenshot showing that you've been successful.

#### Submit: Evidence that MFA is Enabled (Due During Class Period)
Submit a screenshot [showing a successful test of using your token](https://docs.nersc.gov/connect/mfa/#testing-your-new-token).


## Pre-Work (One Week in Advance)
You will complete the following pre-work in class, one week in advance of the lab day.

### (In-Class) Demonstrate Account Login (5 minutes)
In this pre-work, you will verify that are able to log into NERSC and ready for next week's lab.

#### Step-by-Step: Log into NERSC Jupyter Hub

1.  Navigate in a web browser to the [NERSC Jupyter Hub](https://jupyter.nersc.gov).
2.  When prompted, select "Sign in with Federated Identity at NERSC."
3.  At the federated login page, when prompted to "Choose your Institution", select "National Energy Research Scientific Computing Center (NERSC)."
4.  Enter your NERSC username and password. On the next page, enter your multi-factor authentication token (e.g. the six digits from your phone authentication app; no spaces).

#### Show Me: Successful Login
5.  Upon successful login, show your teacher the completed login screen, and then you can logout again.

### (At-Home) Introductory Videos, Readings, and Reflection (2 hours)
In this extensive pre-work, you will watch videos about NERSC and careers in High Performance Computing (HPC). You will then learn about the specifics of the NVIDIA GPU hardware we will use next week. These videos and readings will give you context for possible careers you may never have considered, and will also help you get the most value out of our lab next week.

Once you've watched the videos and completed all readings, you will submit a brief reflection and share this reflection with your classmates.

#### Watch: What is High Performance Computing (HPC)?

High Performance Computing (HPC) facilities are developed and used in industry (Microsoft, Amazon, Google, NVIDIA, etc.) and scientific research teams / government (Department of Energy, Department of Defense, research universities like UCSD, etc.). This lab will be using HPC resources through a government resource called NERSC, located at Berkeley, CA.

Before we get into NERSC and supercomputers, what is HPC in general, and what are some uses? Watch the following video from industry (Microsoft) to find out!

!?[What is HPC? (by Microsoft)](https://www.youtube.com/watch?v=0biElmaDfFs)

#### Watch: NERSC, Supercomputers, and Scientific Computing

In this lab, you'll be logging into a supercomputer named "NERSC Perlmutter". This is a government-owned supercomputer funded through the Department of Energy. There are only a small handful of supercomputers like this around the country!

But what exactly is a supercomputer? Please watch a video introduction to supercomputers before class!

!?[What is a Supercomputer? (Lawrence Livermore National Laboratory)](https://www.youtube.com/watch?v=9M99STmu-vI)

##### (Optional) Dig deeper with these additional videos:

The following videos are optional, if you'd like to dig deeper! You can also come back to these later.

!?[Go on a Tour of a Supercomputer! (University of Wisconsin-Eau Claire)](https://www.youtube.com/watch?v=uxYX8KXdC0g)

!?[What is a Supercomputer? (Argonne National Laboratory)](https://www.youtube.com/watch?v=4xHoWwxdlms)

Visit the [NERSC YouTube page](https://www.youtube.com/@theRealNERSC) for a lot more videos specific to Perlmutter, the supercomputer you'll be using in class!

If you want to dive really deep and are considering exploring a career in HPC: here's a [three-hour crash course in supercomputing](https://www.youtube.com/watch?v=sVLhWWOxjdo&list=PL20S5EeApOSvQK4rPN53MR3EVWN10KULp) from the staff at NERSC. You can actually meet these people if you'd like! Just ask me for their contact information and I'll put you in touch.

#### Watch: Careers in HPC for Computer Scientists

Computer science degrees are valuable and lead to many careers in HPC. Choose **just one video** below to watch, which represent three examples of careers in HPC!

#### Video Option A: I/O Specialist
!?[Careers in HPC: I/O Specialist Elsa Gonsiorowski, Lawrence Livermore National Laboratory, USA](https://www.youtube.com/watch?v=UzlP0w-BWZo)

#### Video Option B: Web & Mobile Applications Manager
!?[Careers in HPC: Web & Mobile Applications Manager, Tracy Brown, TACC, USA](https://www.youtube.com/watch?v=wuXO2Mhnqm0)

#### Video Option C: Application Developer and Outreach
!?[Careers in HPC: Application Developer, HPC Education & Outreach, Weronika Filinger, EPCC, UK](https://www.youtube.com/watch?v=XAfyQjZNAmM)

#### Case Study: NVIDIA A100 GPUs
NERSC Perlmutter contains **7,208 NVIDIA A100 GPUs**.

You will each access one of these GPUs during next week's lab.

##### How are data center GPUs different from home computer GPUs?
The architects of Perlmutter deliberately chose to use the **NVIDIA A100** GPU, and not a gaming GPU like the **NVIDIA GTX 3080** GPU. This is because the A100 GPU is extremely powerful for scientific computation and its entire design is optimized for data centers (rather than for home computer graphics or video games). In fact, the NVIDIA A100 GPU does not have any video output port whatsoever! You literally could not plug your monitor into an NVIDIA A100 GPU.

Note that with each generation of GPUs from NVIDIA and other companies like AMD, there are different models built with different optimizations. Tradeoffs in the design of GPUs include everything we've discussed this semester with relation to tradeoffs in the design of CPUs - performance versus power consumption, specialization vs. generalization, read/write speeds vs. quantity of memory, number of caches and their locations, organization of processor cores, instructions available in the instruction set, pipelining, number of processors, etc. And just like with CPUs, the GPU in your phone will be designed quite differently than the GPU in a data center -- because the benefits of certain tradeoffs are different in these contexts.

##### Watch: YouTube Video by Engadget: NVIDIA's massive A100 GPU isn't for you (10 minutes)
!?[Engadget: NVIDIA's massive A100 GPU isn't for you](https://youtu.be/ig-7Hyd3Klw)

##### Massive Parallelism of the A100
The massive repetition of elements within each A100 GPU reflects the massive parallelism facilitated by this GPU. The diagrams below showcase this parallelism.

![Diagram of the A100 GPU](https://developer-blogs.nvidia.com/wp-content/uploads/2021/guc/gaEfOQD6l3q8p4TzybT7gMVZc8YQkni-0-9ClI9Ei4epE4aHSLjg9-3ON8bkRFZxvm1G-nOCZ9CPy_zqw-EmBWje-sOiSem0oFWA4J7HnhdVdF5RUbrLB7n5-XGKDGznfh6R3xna.png "The A100 GPU layout. There are 108 identical 'SMs' (each of which  themselves are multiprocessors) on this GPU, leading to the repetitive grid appearance. The repetition of many identical elements is indicative of the massive parallelism of a GPU -- all these SMs can do computations in parallel with one another, as can the multiple processors within each SM. Note also that the A100 has two large memory caches - 'L2 Cache' to serve as shared memory between the SMs. The total L2 Cache size is 40 GB for the A100 GPUs you will use in this lab.")

![Diagram of just one of the 108 SMs](https://developer-blogs.nvidia.com/wp-content/uploads/2021/guc/raD52-V3yZtQ3WzOE0Cvzvt8icgGHKXPpN2PS_5MMyZLJrVxgMtLN4r2S2kp5jYI9zrA2e0Y8vAfpZia669pbIog2U9ZKdJmQ8oSBjof6gc4IrhmorT2Rr-YopMlOf1aoU3tbn5Q.png "A zoomed in view of just one of the 108 SMs on this GPU. Even within a single SM, four identical tensor cores do work in parallel with one another. And adjacent to each tensor core, many mathematics units (e.g. FP32, floating-point unit) do computations in parallel with one another. In addition to the processing elements in parallel, note that we have many caches in parallel - in other words, many parallel memory structures.")

##### Time Penalties of Data Transfer to GPUs

There exists physical distance between the GPUs and the two CPUs (silver squares). Therefore, data has to be sent back and forth across the motherboard between the CPU and GPUs. Data transfer incurs a time penalty in your code each time it happens.

![Eight NVIDIA A100 GPUs and two CPUs, all on a single motherboard.](HGX_A100_8_way_3QTR_Front_Left-Edit-1-768x512.jpg "Eight NVIDIA A100 GPUs and two CPUs, all on a single motherboard. The two CPUs are the silver squares to right. Note the physical distance between the GPUs and CPUs, requiring data transfer between them.")

Learn More:

1. [Ampere Architecture](https://developer.nvidia.com/blog/nvidia-ampere-architecture-in-depth/)
2. [NVIDIA A100 PDF](https://images.nvidia.com/aem-dam/en-zz/Solutions/data-center/nvidia-ampere-architecture-whitepaper.pdf)
2. [Introducing NVIDIA HGXA100](https://developer.nvidia.com/blog/introducing-hgx-a100-most-powerful-accelerated-server-platform-for-ai-hpc/)

#### Submit (Due the Day Before Lab): Brief Written Reflection on Videos
Submit a brief reflection on what you just watched and read. What interested you? What surprised you? Elaborate.

Share this reflection on Padlet with your class (TODO) prior to the lab period.

## Introduction

### Activity: Conversation starter
“What did you find surprising? What careers did you see there?”

Then, leads into today’s topic.

### Lecture: Intro to GPU Computing

Lecture outline:

1. Big picture zooming in from everyday phones into a motherboard (RAM, SSD, GPU, …)
2. CPU vs. GPU
3. Massive parallelism
4. Many uses of a GPU in a phone
5. How are a data center, HPC cluster, laptop and similar and different from your phone? (And how are they in-use when you access your phone)
6.	Here’s what it would look like in your phone, laptop, data center, HPC cluster
7.	Here’s what you’d actually use it for in your phone, laptop, data center, HPC cluster?

### Post-Lecture Activities:
Show a GPU, does this go in a server? In a laptop? In a data center?


Show off some GPU chip die shots from Wikichip, try to pick out the GPU.

## Access a GPU on NERSC
### Log into NERSC Jupyter Hub

1.  Navigate in a web browser to the [NERSC Jupyter Hub](https://jupyter.nersc.gov).
2.  When prompted, select "Sign in with Federated Identity at NERSC."
3.  At the federated login page, when prompted to "Choose your Institution", select "National Energy Research Scientific Computing Center (NERSC)."
4.  Enter your NERSC username and password. On the next page, enter your multi-factor authentication token (e.g. the six digits from your phone authentication app; no spaces).

### Start a "Shared GPU" Job
5. From the Jupyter Hub Perlmutter landing page, under **"Shared GPU Node"**, press **"Start"**.
6. After a short wait, you will arrive at a page that includes a "Launcher" tab. Keep this tab open for later.

### Launch "Terminal"
7. From the "Launcher", scroll down all the way to the "Other" section, and select "Terminal". This will open a Linux terminal window, logged into Perlmutter.

### Examine your GPU from the terminal
8. From the terminal, type "nvidia-smi -L" and press Enter. (Note: Capitalization matters in the terminal.) You will see the model of the GPU for the machine you are currently accessing.

```
sfeister@nid001045:/global/u1/s/sfeister> nvidia-smi -L
GPU 0: NVIDIA A100-SXM4-40GB (UUID: GPU-893f36ab-1e28-a964-f03d-38d5b163e038)
```

As you can see from the output above, you are using the NVIDIA A100 GPU that you watched videos and read about earlier in this lab.

9. After you've confirmed your GPU, you can see more stats about its current status. Type "nvidia-smi" (with no flags) and press Enter. You will see more stats for the GPU for the machine you are currently accessing.

``` 
sfeister@nid001045:/global/u1/s/sfeister> nvidia-smi
Tue Aug  8 10:16:44 2023       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 525.105.17   Driver Version: 525.105.17   CUDA Version: 12.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA A100-SXM...  On   | 00000000:03:00.0 Off |                    0 |
| N/A   28C    P0    52W / 400W |      0MiB / 40960MiB |      0%      Default |
|                               |                      |             Disabled |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

10. (Optional) If you want to see even more detailed stats on your GPU, try typing "nvidia-smi -q" and then press "Enter".

## Hello World on your GPU
### What is CUDA?

Watch the two video below to answer the question: "What is CUDA?", and even give an introduction to how it works.

!?[What is CUDA (Roboflow) (1 minute)](https://www.youtube.com/watch?v=vZX0rcJl8o8)

!?[Intro to CUDA, Intro to CUDA - An introduction, how-to, to NVIDIA's GPU parallel programming architecture (5 minutes)](https://www.youtube.com/watch?v=IzU4AVcMFys)

### (Optional, something for later) Follow a CUDA Tutorial

Here are some CUDA tutorials to help you learn more.
1. Easiest: ["CUDA Tutorial" on ReadtheDocs, by Putt Sakdhnagool](https://cuda-tutorial.readthedocs.io/en/latest/)
2. More in-Depth: ["An Even Easier Introduction to CUDA", by Mark Harris](https://developer.nvidia.com/blog/even-easier-introduction-cuda/)
3. Even More-in-Depth: ["CUDA Pro Tip: Write Flexible Kernels with Grid-Stride Loops", by Mark Harris](https://developer.nvidia.com/blog/cuda-pro-tip-write-flexible-kernels-grid-stride-loops/)

I use the above as references in the next few sections, including copying some code exactly from those tutorials.

You may wish to come back and follow these tutorials about CUDA on your own time, later. For now, proceed to the next page. Remember as you go, you can come back here later for more depth.

### Hello World

#### Create a project folder

You may need teacher help to follow along with these steps. I will lead you through this section as a class.
1. In the left-hand panel of JupyterHub, move your cursor under the header of "File Browser".
2. Right click anywhere within the File Browser section to open a drop-down menu with options for creating elements. In that menu, select "New folder".
3. Name your folder something like "GPULab".
4. Navigate into your newly-created folder by double-clicking it.
5. Now that you've navigated into your new folder, right click again anywhere within the File Browser section to open the same drop-down menu. This time, in that menu, select "New File".
6. Name your new file "hello.c". (Note, you'll need to delete the ".txt" extension -- in other words, name your file "hello.c", not "hello.c.txt").
7. Finally, within the File Browser, double click on your newly-created "hello.c" file to open and edit it within a new text editing tab of Jupyter Hub.
8. Paste the following contents into your file, edit it to change "Hello, world" to something more fun like "Hello, Scott!", and save your new file.

```c
void c_hello(){
    printf("Hello World!\n");
}

int main() {
    c_hello();
    return 0;
}
```

9. Compile your c file from the terminal.

## Background Skills
a.	Intro to why you need these: Programming a GPU on a cluster, NERSC
b.	Diagram: here’s what we’ll do:
i.	Our computer  Login to remote machine  Do work on remote machine  Copy results back to our machine
c.	Uses something called Linux shell. Here are some key skills:
i.	(Give them a cheat sheet with limited options to go along with this)
ii.	mkdir, cd (Activity for practice, turn something simple in)
iii.	all about flags
iv.	gcc
v.	nvcc
d.	Cheat sheet tailored to the activity itself – only the stuff for the lab


## Primary Activity: Create an Algorithm

### Activity Overview
a.	Create a simple algorithm for encrypting data
b.	Activity in C – write an encryption and decryption

### Lecture: How do you move something onto a GPU?
a.	Show off a diagram of how we pull it in, send it back out data-wise
i.	Discussion activity: Why do we do this?
b.	Show them my encryption
i.	Show them how I move it to the GPU
c.	Check that the results are still the same as they were

### Move Algorithm onto GPU

1. Open a shared GPU node
TODO

### Run Benchmarks
Run benchmarks (Holy cow! Computation took almost no time, and data took so much time)

### Improve and Re-Run Benchmarks
Make their encryption more elaborate, run again and re-benchmark

## Reflection Activities

### Shared memory reflection activity
(TODO: Needs significant improvement)

Activity: Doing laundry at home versus hiring a laundry service
1.	Which is probably faster at doing each load?
2.	Which will get you your laundry back clean faster, and does it depend on how much laundry you have to do?

Discuss: How is the cost/benefit analysis of doing laundry at home versus hiring a laundry service, similar to using the CPU for computation versus sending data to the GPU?


