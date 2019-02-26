
# Introduction to Rahti

<!-- .slide: data-background="img/topic_background.png" -->

---

## Rahti is a

> container cloud Platform as a Service (PaaS) based on OpenShift - Red Hat's distribution of Kubernetes

&nbsp;
&nbsp;

----

&nbsp;
&nbsp;

### Allows

*Provisioning servers based on container technology with JSON API or web console.*

---

## Containers in Openshift

* Container images contain full Linux software stacks up to kernel
    * "Light weight virtual machines"
* Follow Docker standard $\longrightarrow$ Wide support
    * Build once run everywhere (with small modifications)
* Extension of Kubernetes

**For almost all purposes:**

>Container is an operating system without a kernel packaged in a standardized way

---

## Virtual machine vs. container

![VMs vs. containers](img/vm_vs_container.png)

Note: Native kernel when host is Linux. Uses kernel cgroups and namespaces

---

## Virtual machine vs. container

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

## Defining container images

* A standardized way of defining container images is via Dockerfiles
```Dockerfile
FROM ubuntu:18.04
RUN apt-get update \
    && apt-get install -y --no-install-recommends mysql-client \
    && rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["mysql"]
```
* Start with *base image* (here `ubuntu:18.04`) and
* each line of the Dockerfile creates a *layer* on top of previous
 *image* and only the difference is stored in an *image registry*.

---

## Sample python application

<div id="left">

Pick python template 

</div>

<div id="right">

![vert-shot](img/generic-shots/templates.png)

</div>

---

## Sample python application

<div id="left">

Fill in template details

1. Choose or create project
2. Pick python version (3.6, 3.5, 2.7)
3. Pick name of application
4. Enter application code git repository
    * Click *advanced options* for private repositories
5. Click Create


</div>

<div id="right">

![horiz-shot](img/generic-shots/template-params.png)

</div>

---

## Sample python application

<div id="left">

Click project name on right and wait for the application to be deployed.

</div>

<div id="right">

![horiz-shot](img/generic-shots/template-result.png)

</div>

---

## Sample python application


* When the application us running, OpenShift console will collect data related to it in a dashboard view
* This project has a route http://django-ex-test-python-project.rahtiapp.fi

![horiz-shot](img/generic-shots/template-up.png)


---

## Bringing in your application to Rahti 

<div style="text-align: left">

1. Existing Docker image 
    * Set up routes and services by hand
2. Build Docker image from source
    * Source-to-Image (*Sample python application*)
    * Dockerfile
3. Utilize OpenShift Templates (*Sample python application*)

</div>

===

## Using existing docker image

### Uploading docker image to rahti registry:

1. Create new image stream at [https://registry-console.rahti.csc.fi](Rahti registry console)
2. Follow instructions and login
    * `sudo docker login ...`
    * `oc login ...`
3. Push image to the image stream with Docker
    * Navigate to *Images* and open the newly created image stream tab
    * `sudo docker tag ...`
    * `sudo docker push docker-registry.rahti.csc.fi/...`

===

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
