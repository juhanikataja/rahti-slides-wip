
# Introduction to Rahti

<!-- .slide: data-background="img/topic_background.png" -->

---

## Rahti is a

> container cloud Platform as a Service (PaaS) based on OpenShift - Red Hat's distribution of Kubernetes

<div align="left">

## Allows

</div>

---

## But what's a container

* Everything needed to run an application in one package 
    * "$\inf\sup$" of dependencies for a piece of software
* Standardized software development
    * Build once run everywhere

**For almost all purposes:**

>Container is an operating system without a kernel packaged in a standardized way

---

## What's a Virtual machine vs. container

![VMs vs. containers](img/vm_vs_container.png)

Note: Native kernel when host is Linux. Uses kernel cgroups and namespaces

---

## What's a Virtual machine vs. container

| VM | Container |
|:-|-:|
| Heavy (GBs) | Light (10-1000 MBs)|
| Full OS | Libs and binaries only |
| Persistent | Ephemeral |
| Shouldn't be restarted | Meant to be restarted |
| Slower startup time | Faster startup time |
| Hardware virtualized | Kernel virtualized |
| Any OS | Linux |

---

## Better density of code, less hardware required


![VMs vs. containers](img/vm_container_density.png)

---

## Dockerfile

* A standardized way of defining container images is via Dockerfiles
```Dockerfile
FROM ubuntu:18.04
RUN apt-get update \
    && apt-get install -y --no-install-recommends mysql-client \
    && rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["mysql"]
```
* Roughly speaking: 
    * Start with *base image* (here `ubuntu:18.04`) and
    * each line of the Dockerfile creates a *layer* on top of previous
     *image* and only the difference is stored in an *image registry*.

---

## Docker demo

<div align="left">`Dockerfile`</div>

```Dockerfile
FROM busybox

ENTRYPOINT [ "/bin/telnet", "towel.blinkenlights.nl" ]
```

<div align="left">Shell commands</div>

```bash
docker build . -t starwars:latest
docker images
docker run -it --detach --name starwars starwars
docker ps
clear
docker attach starwars
```

<div style="font-size: 60%"> If you don't have docker installed you can try https://labs.play-with-docker.com </div>

---

## Rahti is a 

> container cloud Platform as a Service (PaaS) based on OpenShift - Red Hat's distribution of Kubernetes

The *container cloud* part
* _Orchestrate_ multiple containers as complex services
    * Better modularity and maintanability &rarr; still see the big picture
* Declare container application as a collection of objects in a text file
    * Parametrizable
    * YAML formatted
* Command line and graphical web interfaces

Note: when containers are run on someone elses hardware and they can be managed systematically

---

## Bringing in your application to Rahti 

> There are 3 trivial ways to bring in your application to Rahti.

* Deploy your application with existing Docker container image
    * Bring in your own Docker formatted container image, or
    * Specify required image from world of Docker Hub 
* Build & deploy you application from source code contained in Git repository
    * Using Source to image (S2I) utility
    * From Dockerfile
* Build in your own complex deployment using OpenShift templates
    * Define your own deployments using YAML, or
    * Browse Redhat's opensourced OpenShift templates

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

# <p style="color:black"> Demos </p>

---

## Demo 1

* Start up an Apache HTTP server serving static content from github
repository https://github.com/CSCfi/rahti-httpd-ex
    * Or you can make your own fork
* Edit the source `index.html`
* Rebuild image
* Debug the running _pod_ on terminal and see that the sources are at
  `/tmp/src`

Note: Show Pods, Services, Routes, Builds, ImageStream and DeploymentConfig

---

## Demo 1: Terminology

* <!-- .element: class="fragment" data-fragment-index="0" -->*Pod*: a collection of containers sharing resources
    * Containers in a pod can talk to each other using `localhost` or shared memory
    * Typically one container per pod
* <!-- .element: class="fragment" data-fragment-index="1" -->*Service*: Object that routes data internally to pods and performs load balancing
* <!-- .element: class="fragment" data-fragment-index="2" -->*Route*: Provides access to a Service from outside
* <!-- .element: class="fragment" data-fragment-index="3" -->*Build*: An object that builds images
* <!-- .element: class="fragment" data-fragment-index="4" -->*ImageStream*: An object that tracks a series of images
* <!-- .element: class="fragment" data-fragment-index="5" -->*DeploymentConfig*: An object that keeps given number of pods alive and manages pod image updates

---

## Demo 2: Command line

* Do the Demo 1 on command line
* Hints: 
    * <!-- .element: class="fragment" data-fragment-index="0" --> Log in 
    * <!-- .element: class="fragment" data-fragment-index="1" -->   `oc get templates -n openshift`
    * <!-- .element: class="fragment" data-fragment-index="2" -->   `oc process --parameters -n openshift <template-name>`
    * <!-- .element: class="fragment" data-fragment-index="3" -->   `oc new-app <template-name>  -p <params>`

Notes: This is only the tip of the iceberg how `oc new-app` works

---

## Demo 3: Apache Spark cluster 

* Set up apache spark cluster with the apache-spark template
* Examine the template source
    * <!-- .element: class="fragment" data-fragment-index="0" --> `oc get templates -n openshift apache-spark -o yaml`

Note: (a) Show scaling of workers. (b) Simple template: `oc get templates -n openshift httpd-example -o yaml`. 

---

# <p style="color:black"> About the platform </p>

---

# <p style="color:black">Why Kubernetes? </p>

---

## Standard

* The de facto standard for container orchestration
* Targeted by software distributors
* Can hire people with Kubernetes skills

---

## Wide support

* Open source, hosted by a foundation (CNCF)
* Backing from tech giants, including:
   * Google, Red Hat, Microsoft, Cisco, Oracle, AWS
* **$10^9$ USD** in investments
* Large ecosystem:
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

## More information

* [The Rahti main page](https://rahti.csc.fi/) for end user documentation
  * Like cPouta and ePouta, you need a CSC computing project to access Rahti
  * No cost for you when you use Rahti for open research and education
  * [Instructions for getting access](https://rahti.csc.fi/introduction/access/)
* [rahti-support@csc.fi](mailto:rahti-support@csc.fi) for support
* [rahti-team@postit.csc.fi](mailto:rahti-team@postit.csc.fi) to contact the team
* [Public roadmap](https://trello.com/b/JQT9QiS2/rahti-container-cloud-roadmap)