# Rahti container cloud service

<!-- .slide: data-background="img/topic_background.png" -->

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

## Rahti

>Is a container orchestration platform that allows running Docker container images.

* OpenShift "community edition": *OKD - The Origin Community Distribution of Kubernetes that powers Red Hat OpenShift.*
* A Kubernetes implementation
    * Kubernetes originally developed at Google
    * Now maintained by Cloud Native Computing Foundation
    * Abbreviated often to ***k8s***
    * OpenShift skills translate to Kubernetes skills and vice versa
* Terms OpenShift and Kubernetes can be used interchangeably, but OpenShift has some additional features that Kubernetes hasn't

---

# Part 2: Running workloads in Rahti

<!-- .slide: data-background="img/topic_background.png" -->

---

## Applications in Kubernetes 

<div class=container>
<div class=col>

* Everything is a Kubernetes API Object 
* Every object is of some *kind* (Pod, Service, Secret, ...)
* Objects have a natural JSON / YAML representation
* Objects typically have some metadata
  * name, labels, ...

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
</div>

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
  * Indentation matters: Use space character (ASCII 0x20), suggestion is 2 spaces

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

## DeploymentConfig

```yaml
apiVersion: v1
kind: DeploymentConfig
metadata:
  labels:
    app: serveapp
  name: servedeployment
spec:
  replicas: 1
  selector:
    app: serveapp
    deploymentconfig: servedeployment
  strategy:
    activeDeadlineSeconds: 21600
    type: Rolling
  template:
    metadata:
      labels:
        app: serveapp
        deploymentconfig: servedeployment
    spec:
      containers:
      - name: serve-cont
        image: "docker-registry.default.svc:5000/openshift/httpd:2.4"
  triggers:
  - type: ConfigChange
```

---

## DeploymentConfig

```yaml
apiVersion: v1
kind: DeploymentConfig
metadata:
  labels:
    app: serveapp
  name: servedeployment
```

```yaml
spec:
  replicas: 1
  selector:
    app: serveapp
    deploymentconfig: servedeployment
  strategy:
    activeDeadlineSeconds: 21600
    type: Rolling
  triggers:
  - type: ConfigChange
```

```yaml
  template:
    metadata:
      labels:
        app: serveapp
        deploymentconfig: servedeployment
    spec:
      containers:
      - name: serve-cont
        image: "docker-registry.default.svc:5000/openshift/httpd:2.4"
```

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

## Service

<div class=container>

<div class=col>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: serve
  labels:
    app: serveapp
spec:
  ports:
  - targetPort: 7000
  selector:
    pool: serveapp
```
</div>

<div class=col>

* Serve traffic to port 7000 of pods with label "pool: serveapp"
* Discoverable by the name "serve" in the namespace
*   One can define name, and inbound port and protocol for the service as well

    ```yaml
    ports:
    - targetPort: 7000
      port: 5000
      name: tcp-5000
      protocol: TCP
    ```

</div>

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

## Route

<div class=container>
<div class=col>

```yaml
apiVersion: v1
kind: Route
metadata:
  labels:
    app: serveapp
  name: myservice
  annotations:
    haproxy.router.openshift.io/ip_whitelist: 192.168.1.0/24 10.0.0.1
spec:
  host: <myservice>.rahtiapp.fi
  to:
    kind: Service
    name: serve
    weight: 100
```

</div>
<div class=col>

* Redirects http/https traffic to Service with name "serve"
* If Service defines multiple ports then define `spec.port.targetPort: 5000` or `tcp-5000`

</div>
</div>

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

## What was not covered - but should've

* `oc new-app`: bake source repository (php, java, nodejs, Dockerfile, ...) in to a container image
* `oc expose`: create route with oneliner
* imageChange trigger in DeploymentConfig: trigger updates when a new image is uploaded to internal registry
* `ImageStream` (OpenShift): Watching image updates in internal registry
* `BuildConfig` (OpenShift): Building images in Rahti
* `CronJob`: running Pod at specific times
* `initContainer`: run-to-completion container executed before other containers in Pod
* `HorizontalPodAutoscaler`: starts up new pods according to server load
* `Template`: Collect number of objects to parametrizable lists

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

## Exercises

Exercises are located at [github.com/CSCfi/rahti-bioweek-2019](https://github.com/CSCfi/rahti-bioweek-2019).

---

