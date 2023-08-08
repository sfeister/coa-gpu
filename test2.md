# GPU Laboratory

In this lab, we will design a simple data encryption algorithm and implement it (and assess its benchmarks) on both a GPU and CPU.

## Learning Outcomes

Upon completing this laboratory, students will:

* Examine separation of GPU memory caches and CPU memory caches (So data transfer across the bus is needed at some step even if the CPU has already been working on the data)
* Examine differences in generality CPU instruction sets and GPU instruction sets
* Demonstrate the massive parallelism of a GPU through kernel-level computer programming
* Explore situations where GPUs are faster, and CPUs are faster, and do fine-grained benchmark to show how memory transfer and GPU clock speed impacts these outcomes
* Showcase one application of GPUs, encryption of data, using CUDA programming

## Pre-Work

### (Two Weeks in Advance) Apply for a NERSC Account

#### Overview of Applying for a NERSC Account
Later this semester, I am going to have everyone in the class access a supercomputer to complete labs relating to parallel processors and GPU computing. I have an award of supercomputing time granted to me from a [government-funded national supercomputer center](https://www.nersc.gov/). This center, called NERSC, is located in San Francisco. We will likely be accessing limited numbers of computing nodes on the [Perlmutter supercomputer](https://www.nersc.gov/systems/perlmutter/). You can [read about the architecture here](https://docs.nersc.gov/systems/perlmutter/architecture/).

Note before proceeding:

> Your account will undergo user vetting, in accordance with NERSC policies, to verify your identity. Under some circumstances, there could be a delay of up to a week while this vetting takes place.

NERSC representatives have assured me this user vetting is lighter than a typical background check, and importantly, does not involve investigation of immigration status. Please reach out to me directly if you'd like more details before proceeding, and I will find out more.

#### Apply for a NERSC Account
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

#### Submit: A Screenshot of Application
Submit a screenshot of your confirmation email showing you have signed up for an account at NERSC.

### (One Week in Advance) Enable Multi-Factor Authentication for Your NERSC Account

NERSC requires multi-factor authentication. You'll install an authenticator app on your phone, and use that app to get a unique "one-time password" (OTP), or "token", each time you login to NERSC. This token is in addition to your regular NERSC password.

The following instructions can be followed only **after your application has been approved** and your NERSC account is active. Approval will taken up to a week. Once you receive an email saying your account has been created, you can continue with these next steps.

#### Enable Multi-Factor Authentication (MFA)
1. Follow the [official NERSC instructions to set up MFA](https://docs.nersc.gov/connect/mfa/).
1. When you get to the section titled "Testing Your New Token", save a screenshot showing that you've been successful.

#### Submit: Evidence that MFA is Enabled
Submit a screenshot [showing a successful test of using your token](https://docs.nersc.gov/connect/mfa/#testing-your-new-token).

### (One Week in Advance) Asynchronous Videos

#### Watch: NERSC, Supercomputers, and Scientific Computing
* “Who we are” cool video

#### Watch: Careers in HPC for Computer Scientists

* “careers in HPC” cool video

#### Case Study: NVIDIA A100 GPUs
NERSC Perlmutter contains **7,208 NVIDIA A100 GPUs**. The architects of Perlmutter chose this model of GPU as it is extremely powerful and designed for data centers (rather than grpahics or video games). In fact, the NVIDIA A100 does not have any video output whatsoever!

##### Watch: YouTube Video by Engadget: NVIDIA's massive A100 GPU isn't for you (10 minutes)
!?[Engadget: NVIDIA's massive A100 GPU isn't for you](https://youtu.be/ig-7Hyd3Klw)

##### Massive Parallelism of the A100
The massive repetition of elements within each A100 GPU reflects the massive parallelism facilitated by this GPU. The diagrams below showcase this parallelism.

![Diagram of the A100 GPU](https://developer-blogs.nvidia.com/wp-content/uploads/2021/guc/gaEfOQD6l3q8p4TzybT7gMVZc8YQkni-0-9ClI9Ei4epE4aHSLjg9-3ON8bkRFZxvm1G-nOCZ9CPy_zqw-EmBWje-sOiSem0oFWA4J7HnhdVdF5RUbrLB7n5-XGKDGznfh6R3xna.png "The A100 GPU Layout - Note the repetition! There are 108 'SMs' on this GPU. The repetition of many identical elements is indicative of the massive parallelism of a GPU.")

![Diagram of just one of the 108 SM100s](https://developer-blogs.nvidia.com/wp-content/uploads/2021/guc/raD52-V3yZtQ3WzOE0Cvzvt8icgGHKXPpN2PS_5MMyZLJrVxgMtLN4r2S2kp5jYI9zrA2e0Y8vAfpZia669pbIog2U9ZKdJmQ8oSBjof6gc4IrhmorT2Rr-YopMlOf1aoU3tbn5Q.png "A zoomed in view of just one of the 108 SM10s on this GPU. Note the Repetion within the SM10 as well!")

##### Time Penalties of Data Transfer to GPUs

There exists physical distance between the GPUs and the two CPUs (silver squares). Therefore, data has to be sent back and forth across the motherboard between the CPU and GPUs. Data transfer incurs a time penalty in your code each time it happens.

![Eight NVIDIA A100 GPUs and two CPUs, all on a single motherboard.](HGX_A100_8_way_3QTR_Front_Left-Edit-1-768x512.jpg "Eight NVIDIA A100 GPUs and two CPUs, all on a single motherboard. The two CPUs are the silver squares to right. Note the physical distance between the GPUs and CPUs, requiring data transfer between them.")

References:

1. [Ampere Architecture](https://developer.nvidia.com/blog/nvidia-ampere-architecture-in-depth/)
2. [Introducing NVIDIA HGXA100](https://developer.nvidia.com/blog/introducing-hgx-a100-most-powerful-accelerated-server-platform-for-ai-hpc/)


#### Submit: Brief Written Reflection on Videos
Submit a brief reflection on what you just watched and read. What surprised you? Elaborate.

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
TODO - have them watch a video

### (Optional, for Later) Follow a CUDA Tutorial

You may wish to come back and follow more tutorials about CUDA on your own time later.

Here are some CUDA tutorials to help you learn more.
1. Easiest: ["CUDA Tutorial" on ReadtheDocs, by Putt Sakdhnagool](https://cuda-tutorial.readthedocs.io/en/latest/)
2. More in-Depth: ["An Even Easier Introduction to CUDA", by Mark Harris](https://developer.nvidia.com/blog/even-easier-introduction-cuda/)
3. Even More-in-Depth: ["CUDA Pro Tip: Write Flexible Kernels with Grid-Stride Loops", by Mark Harris](https://developer.nvidia.com/blog/cuda-pro-tip-write-flexible-kernels-grid-stride-loops/)

I use the above as references in the next few sections, including copying some code exactly from those tutorials.

For now, proceed to the shorter tutorial that follows here.

### Hello World

void c_hello(){
    printf("Hello World!\n");
}

int main() {
    c_hello();
    return 0;
}

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


