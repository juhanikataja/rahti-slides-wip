# Introduction to Rahti

<!-- .slide: data-background="img/topic_background.png" -->


---

<!-- .slide: center="true" -->

## What is Rahti?

* Container cloud platform based on **OpenShift** - Red Hat's distribution of **Kubernetes**
* Run applications packaged as **containers**

---

## Status of Rahti

* Currently in **closed beta**
* **Production in 2019** - open beta some time before that
* Open beta in spring 2019

---

## What's a container?

* Standardized software development
    * Build once run everywhere
* Everything needed to run an application in one package 

**For almost all purposes:**

>Container is an operating system without a kernel packaged in a standardized way

---

## What's a container vs. Virtual machine

![VMs vs. containers](img/vm_vs_container.png)

---

## Why containers?

* Package highly customized software into **easily** re-usable parts
* Lighter than virtual machine 
    * Sometimes called *light weight virtual machine*
* **Orchestrate** multiple containers as complex services
    * Better modularity and maintanability of complex services
    * ...and still see the big picture

---

# Rahti demo

<!-- .slide: data-background="img/topic_background.png" -->

---

## Virtual machines vs. containers

![VMs vs. containers](img/vm_vs_container.png)

---

## Better density, less hardware needed

![VMs vs. containers](img/vm_container_density.png)

---

## Cloud computing platforms

* **Isolated** computing resources from a **shared pool**
* Self-service
* Users run their own software on the **platform**

---

## Two types of clouds

* <!-- .element: class="fragment" data-fragment-index="0" --> Infrastructure-as-a-service (Pouta) - central concept: **Virtual machines**
* <!-- .element: class="fragment" data-fragment-index="1" --> Platform-as-a-service (Rahti) - central concept: **Applications**
* <!-- .element: class="fragment" data-fragment-index="2" --> Same end goal: **enable users to run their own software in the cloud**

---

## Cloud platform features

|                    | Pouta | Rahti |
|--------------------|:-----:|:-----:|
| Self-service       | ✓     | ✓     |
| REST API           | ✓     | ✓     |
| Persistent storage | ✓     | ✓     |
| Network isolation  | ✓     | ✓     |
| Load balancing     | DIY   | ✓     |
| TLS                | DIY   | ✓     |
| Fault tolerance    | DIY   | ✓     |
| Autoscaling        | DIY   | ✓     |

---

# Simplified workflow example

<!-- .slide: data-background="img/topic_background.png" -->

---

<!-- .slide: data-transition="none" -->
![Container orchestration workflow](img/container_orchestration_stage0.png)

---

<!-- .slide: data-transition="none" -->
![Container orchestration workflow](img/container_orchestration_stage1.png)

---

<!-- .slide: data-transition="none" -->
![Container orchestration workflow](img/container_orchestration_stage2.png)

---

<!-- .slide: data-transition="none" -->
![Container orchestration workflow](img/container_orchestration_stage3.png)

---

<!-- .slide: data-transition="none" -->
![Container orchestration workflow](img/container_orchestration_stage4.png)

---

# Why Kubernetes?

<!-- .slide: data-background="img/topic_background.png" -->

---

## Standard

* The de facto standard for container orchestration
* Targeted by software distributors
* Can hire people with Kubernetes skills

---

## Wide support

* Open source, hosted by a foundation (CNCF)
* Backing from tech giants, including:
   * Google
   * Red Hat
   * Microsoft
   * Cisco
   * Oracle
   * AWS
* **\$4 billion** in investments

---

## Large ecosystem

* <a href="http://l.cncf.io" data-preview-link>CNCF Cloud Native Landscape (https://l.cncf.io)</a>
* <a href="https://kubernetes.io/case-studies/" data-preview-link>Kubernetes Case Studies</a>
---

## Supported by all major cloud providers

* "The K stands for Kubernetes" - Kubernetes on the big three cloud platforms
  * Amazon EKS
  * Microsoft Azure AKS
  * Google GKE

---

### One of the most active open source projects

![TOP 30 open source projects](img/top30-opensource-projects.png)

---

## Sites that run on Kubernetes

![New York Times](img/ny_times_logo.png)
![GitHub](img/github_logo.png)
![Spotify](img/spotify_logo.png)

---

# How to start using Rahti?

<!-- .slide: data-background="img/topic_background.png" -->

---

## More information

* [The Rahti main page](https://rahti.csc.fi/) for end user documentation
  * Like cPouta and ePouta, you need a CSC computing project to access Rahti
  * No cost for you when you use Rahti for open research and education
  * [Instructions for getting access](https://rahti.csc.fi/introduction/access/)
* [rahti-support@csc.fi](mailto:rahti-support@csc.fi) for support
* [rahti-team@postit.csc.fi](mailto:rahti-team@postit.csc.fi) to contact the team
