# Rahti container cloud service

<!-- .slide: data-background="img/topic_background.png" -->

---

## Aim of this afternoon:

<!-- aragorn output {{{ -->
```bash
$ aragorn GCF_000002945.1_ASM294v2_genomic.fna
------------------------------
ARAGORN v1.2.38   Dean Laslett
------------------------------

Please reference the following paper if you use this
program as part of any published research.

Laslett, D. and Canback, B. (2004) ARAGORN, a
program for the detection of transfer RNA and
transfer-messenger RNA genes in nucleotide sequences.
Nucleic Acids Research, 32;11-16.


Searching for tRNA genes with no introns
Searching for tmRNA genes
Assuming circular topology, search wraps around ends
Searching both strands
Using standard genetic code


NC_003424.3 Schizosaccharomyces pombe chromosome I, complete sequence
5579133 nucleotides in sequence
Mean G+C content = 36.1%

1.



               c
             g-c
             g-c
             c-g
             t-a
             t-a
             c-g
             g-c     ct
            t   tcccc  a
     ga    g    !!!!!  g
    t  tgtg     agggg  c
    g  +!!+     c    tt
    g  gcat     t
     ta         g
            a-tg
            c-g
            t-a
            t-a
            c-g
            g-c
           t   t
           t   g
            tgg


    tRNA-Pro(tgg)
    72 bases, %GC = 58.3
    Sequence [365155,365226]



2.



               a
             a-t
             g-c
             t-a
             c-g
             c-g
             c-g
             g-c     ct
            t   ggccc  a
     ga    g    !!!!!  g
    t  tctt     ccggg  c
    g  :!!:     c    tt
    g  tgat     t
     ta         g
            t-ag
            t-a
            c-g
            t-a
            c-g
            c-g
           t   c
           t   a
            cac


    tRNA-Val(cac)
    72 bases, %GC = 56.9
    Sequence [446000,446071]

    .
    .
    .

tRNA anticodon frequency
AAA Phe       AGA Ser       ATA Tyr       ACA Cys
GAA Phe  1    GGA Ser       GTA Tyr  1    GCA Cys
TAA Leu  1    TGA Ser  1    TTA Stop      TCA SeC
CAA Leu       CGA Ser       CTA Pyl       CCA Trp  1

AAG Leu       AGG Pro       ATG His       ACG Arg
GAG Leu       GGG Pro       GTG His  1    GCG Arg
TAG Leu  1    TGG Pro  1    TTG Gln  1    TCG Arg  1
CAG Leu       CGG Pro       CTG Gln       CCG Arg

AAT Ile       AGT Thr       ATT Asn       ACT Ser
GAT Ile  1    GGT Thr       GTT Asn  1    GCT Ser  1
TAT Ile       TGT Thr  1    TTT Lys  1    TCT Arg  1
CAT Met  3    CGT Thr       CTT Lys       CCT Arg

AAC Val       AGC Ala       ATC Asp       ACC Gly
GAC Val       GGC Ala       GTC Asp       GCC Gly
TAC Val  1    TGC Ala  1    TTC Glu  1    TCC Gly  1
CAC Val       CGC Ala       CTC Glu       CCC Gly

tRNA codon frequency
TTT Phe       TCT Ser       TAT Tyr       TGT Cys
TTC Phe  1    TCC Ser       TAC Tyr  1    TGC Cys
TTA Leu  1    TCA Ser  1    TAA Stop      TGA SeC
TTG Leu       TCG Ser       TAG Pyl       TGG Trp  1

CTT Leu       CCT Pro       CAT His       CGT Arg
CTC Leu       CCC Pro       CAC His  1    CGC Arg
CTA Leu  1    CCA Pro  1    CAA Gln  1    CGA Arg  1
CTG Leu       CCG Pro       CAG Gln       CGG Arg

ATT Ile       ACT Thr       AAT Asn       AGT Ser
ATC Ile  1    ACC Thr       AAC Asn  1    AGC Ser  1
ATA Ile       ACA Thr  1    AAA Lys  1    AGA Arg  1
ATG Met  3    ACG Thr       AAG Lys       AGG Arg

GTT Val       GCT Ala       GAT Asp       GGT Gly
GTC Val       GCC Ala       GAC Asp       GGC Gly
GTA Val  1    GCA Ala  1    GAA Glu  1    GGA Gly  1
GTG Val       GCG Ala       GAG Glu       GGG Gly

Number of tRNA genes = 23
tRNA GC range = 30.1% to 46.6%
Number of tmRNA genes = 0




4 sequences searched
Total tRNA genes = 176
Total tmRNA genes = 0
Configuration: aragorn GCF_000002945.1_ASM294v2_genomic.fna
```

<!-- }}}-->

---

# Part 1: Background

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


## Containers 

Container is a mechanism which encapsulates a vanilla collection of Linux resources for an application to use:

---

## Containers 

Own **network**, filesystem, process ids, user ids

```bash
/ $ ifconfig
eth0      Link encap:Ethernet  HWaddr 0A:58:0A:80:06:72
          inet addr:10.128.6.114  Bcast:10.128.7.255  Mask:255.255.254.0
          inet6 addr: fe80::d4d4:38ff:fe5e:6e2b/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1450  Metric:1
          RX packets:8 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:656 (656.0 B)  TX bytes:656 (656.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

Note: alpine image

---

## Containers 

Own network, **filesystem**, process ids, user ids

```bash
sh-4.2$ ls
anaconda-post.log  bin	data  dev  etc	home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

Note: centos:7 image

---

## Containers 

Own network, filesystem, **process ids** and **user ids**, ...

```bash
sh-4.2$ ps axu
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
1016530+      1  1.2  0.0  11680  1168 ?        Ss   10:49   0:00 sh -c (tail -f /dev/null)
1016530+      7  0.0  0.0   4396   356 ?        S    10:49   0:00 tail -f /dev/null
1016530+      8  0.3  0.0  11816  1700 ?        Ss   10:49   0:00 /bin/sh
1016530+     15  0.0  0.0  51740  1732 ?        R+   10:49   0:00 ps axu
```

> Rahti does not allow running containers as root. It always assigns varying user id. This is to prevent security issues.

Note: centos:7 image

---

## Containers

<div class=container>

<div class=col>

* They have a look and feel of a light weight virtual machine, but they are not virtual machines
* Rely on Linux kernel features
* Standardized container *images*
    * Build once run everywhere
* Only Linux based images
* Standards: Docker, rkt, LXC, Singularity, katacontainers, Intel clear containers
* **Rahti supports *Docker* images**

</div>

<div class=col>

![vm-vs-container](img/vm_vs_container.png)

</div>

</div>

---

## Containers enable

* Running software with conflicting requirements on same server
* Run "Ubuntu" software stack on CentOS host
* Security hardening
  * Expose minimal amount of data to container
  * Smaller container image $\rightarrow$ smaller attack surface $\rightarrow$ easier to maintain

>Demo: Docker CLI shell

---

## Rahti

>Is a container orchestration platform that allows running Docker container images.

* OpenShift "community edition": *OKD - The Origin Community Distribution of Kubernetes that powers Red Hat OpenShift.*
* A Kubernetes implementation
    * Kubernetes originally developed at Google
    * Now maintained by Cloud Native Computing Foundation
    * OpenShift skills translate to Kubernetes skills and vice versa
* Terms OpenShift and Kubernetes can be used interchangeably, but OpenShift has some additional features that Kubernetes hasn't

---

## Rahti use cases

* Databases
* Web services
* Computation
* Weird software stacks
* High Availability services
* Anything that runs as a container
* One shot runs ($\leftarrow$ today's usecase)
* Anything that runs in a container and requires modest amount cpu/ram/disk
  * #(cpu) $\lessapprox 2$
  * RAM $\lessapprox 8$ GB
  * Disk $\lessapprox 100\dots1000$ GB

---

# Part 2: Running workloads in Rahti

<!-- .slide: data-background="img/topic_background.png" -->

---

## Running containers in Kubernetes: Pods

<div class=container>

<div class="col">

![pod architecture](img/pods-and-storage-nophys.svg)

</div>

<div class="col">

* Pod manages multiple containers
  * Announces mountable volumes from persistent storage claims
  * They all run physically near each other
  * Containers in a pod share IP and memory
* Data in containers is ephemeral, container is reset when it is killed and restarted
  * Root volume is locate at the compute node: SSD disk, no redundancy
* Persistent disk using volume mounts

</div>

</div>

---

## Running containers in Kubernetes: Pods

<div class=container>
<div class="col">

![pod architecture](img/pods-and-storage.svg)

</div>

<div class="col">

* Pod manages multiple containers
  * Announces mountable volumes from persistent storage claims
  * They all run physically near each other
  * Containers in a pod share IP and memory
* Data in containers is ephemeral, container is reset when it is killed and restarted
  * Root volume is locate at the compute node: SSD disk, no redundancy
* Persistent disk using volume mounts

</div> </div>

---

## Object definitions in Kubernetes

<div style="text-align: left">

* Objects are defined as key-value maps
* Representation in YAML language
  * Indentation matters, no tabs, suggestion is 2 spaces

</div>

<div class=container>
<div class=col>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple
  labels:
    job: analyze
spec:
  volumes:
  - name: volume-a
    persistentVolumeClaim:
      claimName: pvc-a
  containers:
  - name: container-a
    image: centos:7
    volumeMounts:
    - mountPath: /data
      name: volume-a
``` 

</div>

<div class=col>

![one volume pod](img/easypod.svg)

</div> </div>

$\downarrow$

===

## Brief intro to YAML files

YAML is a intermediate data language based on key-value pairs and lists:

<ul> <li> Just a value is a YAML file

```yaml
"this is a valid yaml file"
```

</li>

<li> Key and value is signified with colon ":" (Value must be indented!)

<div class=container> <div class=col>

```yaml
key: 
  value
```

</div> <div class=col style="max-width: 50px; margin-top: 10px; ">
$\Leftrightarrow$
</div>

<div class=col>

```yaml
key: value
```

</div> </div> </li>

<li> Lists are written with "[" and "]" or with "-" symbols:

<div class=container> 

<div class=col style="max-width: 280px">

```yaml
list:
- value 1
- value 2
```

</div> 

<div class=col style="max-width: 40px; margin-top: 10px">
$\Leftrightarrow$
</div>

<div class=col style="max-width: 280px">

```yaml
list:
  - value 1
  - value 2
```

</div> 

<div class=col style="max-width: 40px; margin-top: 10px">
$\Leftrightarrow$
</div>

<div class=col>

```yaml
list: [value 1, value 2]
```

</div> </div> </li> </ul>

$\downarrow$

===

## Brief intro to YAML files

* Combining these we get hierarchical structures:

    ```yaml
    key:
      subkey:
        value of subkey
      subkey-2:
        value of subkey-2
      subkey-3:
      - this
      - is
      - a 
      - list
    key-2: value for key-2
    ```

---

## Object definitions in Kubernetes: Pods

<div id="left">

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple
  labels:
    job: analyze
```

```yaml
spec:
```


```yaml
  volumes:
  - name: volume-a
    persistentVolumeClaim:
      claimName: pvc-a
```

```yaml
  containers:
  - name: container-a
    image: centos:7
    volumeMounts:
    - mountPath: /data
      name: volume-a
``` 

</div>

<div id="right">

* Header:
  * Which version of API?
  * Kind of the object
  * Assign it a name and some labels
* Specification of the Pod
  * Define volumes to be brought to the Pod
  * Define containers in the pod
    * There can be multiple, this is a list!
    * Define where the volume is mounted in the container

</div>

---

## How to submit a pod to rahti?

* Use the `oc` command line tool
* Write the yaml-file
* Submit by
```bash
oc create -f pod.yaml
```

>Demo: Submitting Pod to Rahti

---

## Did it work?

* Web console
* `oc describe pod simple`

---

## Persistent volume claims - How to claim storage from the storage cluster?

---

## Web console

![storage-1-2](img/storage/storage-1-2.png)

---

## Web console

![storage-3](img/storage/storage-3.png)

---

## Using YAML specification file

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-a
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

## Back to the Pod demo

*Does it work now?*

```
$ oc describe pod simple
...
Events:
  Type     Reason            Age               From                         Message
  ----     ------            ----              ----                         -------
  Warning  FailedScheduling  1m (x15 over 4m)  default-scheduler            persistentvolumeclaim "pvc-a" not found
  Normal   Scheduled         27s               default-scheduler            Successfully assigned simple to rahti-comp-io-s5-5
  Normal   Pulling           4s (x3 over 24s)  kubelet, rahti-comp-io-s5-5  pulling image "centos:7"
  Normal   Pulled            2s (x3 over 21s)  kubelet, rahti-comp-io-s5-5  Successfully pulled image "centos:7"
  Normal   Created           2s (x3 over 21s)  kubelet, rahti-comp-io-s5-5  Created container
  Normal   Started           1s (x3 over 21s)  kubelet, rahti-comp-io-s5-5  Started container
  Warning  BackOff           1s (x3 over 17s)  kubelet, rahti-comp-io-s5-5  Back-off restarting failed container
```
<!-- .element: class="fragment" data-fragment-index="0" -->

* OpenShift will run the container over and over again.
<!-- .element: class="fragment" data-fragment-index="0" -->

*But there's nothing to execute.*
<!-- .element: class="fragment" data-fragment-index="0" -->

**We can specify `command` to run in the container.**
<!-- .element: class="fragment" data-fragment-index="1" -->

---

## The `command` specification

<div class="container">

<div class="col">

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple
  labels:
    job: analyze
spec:
  volumes:
  - name: volume-a
    persistentVolumeClaim:
      claimName: pvc-a
  containers:
  - name: container-a
    image: centos:7
    volumeMounts:
    - mountPath: /data
      name: volume-a
    command:
    - sh
    - -c
    - (tail -f /dev/null)
```

</div>

<div class="col">

* Defines *ENTRYPOINT* of the container
* Each entry of the `command` array is the *n* th argument. Here:
  * "`sh`" is the 0th argument (command to execute)
  * "`-c`" is the 1st argument
  * "`(tail -f /dev/null)`" is the 2nd argument
* Equivalent with
```bash
sh -c '(tail -f /dev/null)'
```
* Parentheses start a sub-shell so `tail` wont run with process id 1

</div>

</div>

Edit the pod definition and `replace` it. Does it work now?

---

## Debug and file transfer

See if the pod is up and running.

```bash
$ oc get pod
NAME      READY     STATUS    RESTARTS   AGE
simple    1/1       Running   0          1m
```

Remote shell connection to container, create file in the persistent volume mount:

```bash
$ oc rsh simple
sh-4.2$ echo test > /data/testfile
sh-4.2$ exit
```

Copy `testfile` to local shell:

```bash
$ oc rsync simple:/data/testfile ./
WARNING: cannot use rsync: rsync not available in container
testfile
```

---

## A typical pattern in the `command` specification

```yaml
command: 
- sh
- -c
- > 
  echo first command &&
  echo second command &&
  echo third command
```

Is equivalent with

```bash
sh -c 'echo first command && echo second command && echo third command'
```

---

## Run-once-Pod

<div class=container>

<div class=col>

* OpenShift will try to run the pod again if it exits
* Use "`restartPolicy: Never`" in the container definition for run-once-containers
* Output of the pod:

```bash
$ oc logs simple
Short payload
```

</div>

<div class=col>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple
  labels:
    job: analyze
spec:
  restartPolicy: Never
  volumes:
  - name: volume-a
    persistentVolumeClaim:
      claimName: pvc-a
  containers:
  - name: container-a
    image: centos:7
    volumeMounts:
    - mountPath: /data
      name: volume-a
    command:
    - sh
    - -c
    - echo Short payload
```

</div>

</div>

---

## The `oc` tool

>Get help on `<command>`: `oc <command> --help`

| Syntax | Meaning |
|--------|-------------|
| `oc create -f <fileName>` | Create object from file |
| `oc replace [--force] -f <fileName>` | Replace object with <fileName>. Use `force` to delete old first. |
| `oc delete <objectType> <objectName>` | Delete object from cluster |
| `oc describe <objectType> <objectName>` | Display object status |
| `oc logs <podName> [-c <containerName>]` | output stdout of pod `<podName>`, optionally that of container `<containerName>` |

$\downarrow$

===

$\uparrow$


| Syntax | Meaning |
|--------|-------------|
| `oc status` | Display current OpenShift top level project status |
| `oc explain <objectType>.<field>.<subField>` | Print out documentation |
| `oc rsync <pod>:<filePath> <localPath>` | Copy data from/to pod to/from local filesystem |
| `oc rsh <pod>` | Remote shell to container |
| `oc projects` | Show projects |
| `oc project <name>` | Switch to project `<name>` |
| `oc new-project <name>` | Create new OpenShift project `<name>` |
| `oc get <objectType> [<objectName>]` | Get object information |


---

## OpenShift Project concept

* OpenShift "projects" are namespaces for the Kubernetes Objects
* In single namespace there may be single object of given type-name-combination
* By default objects are not visible across projects
* Controlled with following commands:

| Syntax | Meaning |
|--------|-------------|
| `oc projects` | Show projects |
| `oc project <name>` | Switch to project `<name>` |
| `oc new-project <name>` | Create new OpenShift project `<name>` |

---

## Summary

* Rahti runs Docker containers
* Containers are *ephemeral*
* Persistent storage must be requested and mounted to containers
* Pod is the OpenShift object that manages containers
* OpenShift objects are created from YAML files with `oc create -f <filename>`
* Define `command` in the container specification to run specific binary 
    * Otherwise the image's default command is executed
* Projects/namespaces isolate applications

---

## Exercises

Exercises are located at [github.com/CSCfi/rahti-bioweek-2019](https://github.com/CSCfi/rahti-bioweek-2019).

---

# Part 3: More OpenShift

<!-- .slide: data-background="img/topic_background.png" -->

---

## Short security guide

* Always review your container images
  * Use curated image sources (e.g. biocontainers.pro)
* For servers use IP whitelisting when possible
* Keep webservices shortlived if possible
  * Remember that you are the webmaster

---

## Resource requests and limits


<div class=container>
<div class=col>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple
  labels:
    job: analyze
spec:
  restartPolicy: Never
  containers:
  - name: container-a
    image: centos:7
    command: ["sh", "-c", "echo Hello"]
    resources:
      requests:
        memory: "200M"
        cpu: "200m"
      limits:
        memory: "200M"
        cpu: "200m"
```

</div>

<div class=col>

* Use `spec.containers.resources` to specify how much resources to reserve.
* Fractions of CPU are possible: "200 millicores"
* Memory: M for Megabytes, G for Gigabytes
* Define only limit $\rightarrow$ Kubernetes assigns equal requests
* Billing is done according to requests
* If not request/limit is in place default ones are chosen
  * CPU: 100 millicores / 2 cores
  * Memory: 200 MiB / 8 GiB

</div>

---

## Running server jobs in Rahti

<div class=container>
<div class=col style="min-width: 50%" >

Problem

1. The Pod IP addresses are subject to change
2. Pods are shut down if the node running them fails
3. The Pod IPs are not visible to internet
4. Load balancing
5. Updating pods causes service downtime
6. Passwords or private keys in container images
7. Container image per configuration

</div>
<div class=col>

Solution

1. `Service` or `StatefulSet`
2. Controllers
3. `Route` (OpenShift)
4. `Service`
5. `DeploymentConfig` (OpenShift) or `Deployments`
6. `Secret` 
7. `ConfigMap`

</div>
<!-- .element: class="fragment" data-fragment-index="0" -->
</div>

Note: for every problem there is an object that solves it

---

## Service

<div class=rcontainer>
<div class=row>

Solves problems 1 and 4: Pod IPs need to be tracked and traffic needs load-balancing

</div> 
<div class=row style="max-height: 600px">

<img src="img/service.svg" alt="service"/>

</div> </div>

---

## Route

Roundabouts problem 3: " The Pod IPs are not visible to internet" by routing HTTP traffic to Service object in the cluster.

<div class=container>

<div class=row>


* Automatic route with hostnames `<hostname>.rahtiapp.fi`
* TLS encryption provided via rahtiapp.fi domain
* Any hostname possible, user needs to keep track of DNS and CA certificates
* Supports IP whitelisting

</div> 

<div class=row style="max-height: 400px">

<img src="img/route.svg" alt="Route"/>

</div> </div>

---


## Controllers

* Controllers are a class of objects that start pods according to specific rules
* Pod definitions are in the controllers' spec as a template
* `ReplicaSet`, `ReplicationController`, `Deployments`, `DeploymentConfig`, `StatefulSet`, `CronJob`, ...
* They *Control* pods
* They all solve Problem 2: "Pods are shut down if the node running them fails"

Note: Special case: ReplicationController and ReplicaSet

---

## ReplicationController & ReplicaSet

<div class=rcontainer>

<div class=row>

Controllers that keep matching pods alive.

</div> 

<div class=row style="max-height: 600px">

<img src="img/replicationcontroller.svg" alt="ReplicationController"/>

</div> </div>


---

## StatefulSet

<div class=rcontainer>

<div class=row>

Controller that keeps unique pods alive and gives them always unique names. Hostnames: `web-0..n`.

</div> 

<div class=row style="max-height: 600px">

<img src="img/statefulset.svg" alt="StatefulSet"/>

</div> </div>

---

## Deployments / DeploymentConfig

<div class=rcontainer>

<div class=row>

* Create `ReplicaSet`s (`Deployments`) and `ReplicationController`s (`DeploymentConfig`)
* Automates application upgrades 
* `DeploymentConfigs` can watch when new container images appear in the internal image registry
* `Deployment` is generic Kubernetes object and `DeploymentConfig` is an OpenShift extension

</div> 

<div class=row style="max-height: 300px">

<img src="img/deployment.svg" alt="Deployment"/>

</div> </div>

---

## Secrets and ConfigMaps

<div class=container>

<div class=col>

* `Secret` and `ConfigMap`
  * Environment variable
  * Volume mount: Create files according to keys, populate contents according to value

</div> 

<div class=col>

<img src="img/configmount.svg" alt="Secret"/>

</div> </div>

---

## And much more!

* `ImageStream` (OpenShift): Watching image updates in internal registry
* `BuildConfig` (OpenShift): Building images in Rahti
* `CronJob`: running Pod at specific times
* `initContainer`: run-to-completion container executed before other containers in Pod
* `HorizontalPodAutoscaler`: starts up new pods according to server load
* `Template`: Collect number of objects to parametrizable lists

Note: Show template demo

---

## Rahti links

* [The Rahti main page](https://rahti.csc.fi/) for end user documentation
  * You need a CSC computing project to access Rahti
  * No cost for you when you use Rahti for open research and education
  * [Instructions for getting access](https://rahti.csc.fi/introduction/access/)
* [rahti-support@csc.fi](mailto:rahti-support@csc.fi) for support
* [Public roadmap](https://trello.com/b/JQT9QiS2/rahti-container-cloud-roadmap)
* External documentation
  * [Kubernetes documentation](https://kubernetes.io/docs/home/)
  * [OpenShift documentation](https://docs.okd.io/)

---

