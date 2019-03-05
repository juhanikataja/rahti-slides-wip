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

## Containers 

* Container is a mechanism which encapsulates an unused set of Linux resources for an application to use:
    * Own network, filesystem, process ids, user ids, resource quota
* They have a look and feel of a light weight virtual machine like in Pouta, but they are not virtual machines.
* Standardized container *images*.
    * Build once run everywhere.
    * But avoid some pitfalls.
* Standards: Docker, rkt, LXC, Singularity, Intel Clear Containers
* **Rahti supports Docker images**

---

## Containers enable

* Running software with conflicting requirements on same server
* "Ubuntu" on CentOS
* Security hardening

>Demo: Docker CLI shell

---

## Rahti

>Is a container orchestration platform that allows running Docker container images.

* OpenShift "community edition", currently version 3.10
* A Kubernetes implementation
    * Kubernetes originally from Google
    * Now maintained by Cloud Native Computing Foundation
    * OpenShift skills translate to Kubernetes skills and vice versa

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

## Running containers in Kubernetes: Pods

<div class=container>

<div class="col">

![pod architecture](img/pods-and-storage-nophys.svg)

</div>

<div class="col">

* Pod manages multiple containers. 
  * Announces mountable volumes from persistent storage claims
  * They all run physically near each other.
  * Containers in a pod share IP and memory.
* Data in containers is ephemeral, container is reset when it is killed and restarted
  * Root volume is locate at the compute node: SSD disk, no redundancy
* Persistent disk using volume mounts.

</div>

</div>
---

## Running containers in Kubernetes: Pods

<div class=container>
<div class="col">

![pod architecture](img/pods-and-storage.svg)

</div>

<div class="col">

* Pod manages multiple containers. 
  * Announces mountable volumes from persistent storage claims
  * They all run physically near each other.
  * Containers in a pod share IP and memory.
* Data in containers is ephemeral, container is reset when it is killed and restarted
  * Root volume is locate at the compute node: SSD disk, no redundancy
* Persistent disk using volume mounts.

</div> </div>

---

## Object definitions in Kubernetes

<div style="text-align: left">

* Objects are defined as key-value maps
* Representation in YAML language
  * Indentation matters
  * Press down for intro to YAML

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
    image: alpine
    volumeMounts:
    - mountPath: /data
      name: volume-a
``` 

</div>

<div class=col>

![one volume pod](img/easypod.svg)

</div> </div>

===

## Brief intro to YAML files

* YAML is a intermediate data language based on key-value pairs and lists:
    
* Just a value is a YAML file

    ```yaml
    "this is a valid yaml file"
    ```

* Key and value is signified with colon ":" (Value must be indented!)

    ```yaml
    key: 
      value
    ```

* Lists are written with "[" and "]" or with "-" symbols:

    ```yaml
    list:
    - value 1
    - value 2
    ```

    is equivalent to 

    ```yaml
    list: [value 1, value 2]
    ```

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

* Lists as values don't need to be indented (but they can be)
* Value can be on the same line if its not key-value data

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
    image: alpine
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
    * Define where the volume is mounted in the container.
    * Here we could define command to run inside the container

</div>

---

## How to submit the pod to rahti?

* Use the `oc` command line tool.
* Write the yaml-file
* Submit by
```bash
oc create -f pod.yaml
```

>Demo: Submitting Pod to Rahti

---

## Did it work well?

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
Events:
  Type     Reason            Age               From                         Message
  ----     ------            ----              ----                         -------
  Warning  FailedScheduling  1m (x15 over 4m)  default-scheduler            persistentvolumeclaim "pvc-a" not found
  Normal   Scheduled         27s               default-scheduler            Successfully assigned simple to rahti-comp-io-s5-5
  Normal   Pulling           4s (x3 over 24s)  kubelet, rahti-comp-io-s5-5  pulling image "alpine"
  Normal   Pulled            2s (x3 over 21s)  kubelet, rahti-comp-io-s5-5  Successfully pulled image "alpine"
  Normal   Created           2s (x3 over 21s)  kubelet, rahti-comp-io-s5-5  Created container
  Normal   Started           1s (x3 over 21s)  kubelet, rahti-comp-io-s5-5  Started container
  Warning  BackOff           1s (x3 over 17s)  kubelet, rahti-comp-io-s5-5  Back-off restarting failed container
```
<!-- .element: class="fragment" data-fragment-index="0" -->

* OpenShift will run the container over and over again.
<!-- .element: class="fragment" data-fragment-index="0" -->

*But there's nothing to run.*
<!-- .element: class="fragment" data-fragment-index="0" -->

**We can specify `command` to to run in the container.**
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
    image: alpine
    volumeMounts:
    - mountPath: /data
      name: volume-a
    command:
    - sh
    - -c
    - tail -f /dev/null
```

</div>

<div class="col">

* Defines *ENTRYPOINT* of the container
* Each entry of the `command` array is the *n* th argument. Here:
  * "`sh`" is the 0th argument (command to execute)
  * "`-c`" is the 1st argument
  * "`tail -f /dev/null`" is the 2nd argument
```bash
sh -c 'tail -f /dev/null'
```

</div>

</div>

Edit the pod definition and `replace` it. Does it work now?

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

## Detour on `oc` commands

| Syntax | Meaning |
|--------|-------------|
| `oc create -f <filename>` | Create object from file |
| `oc replace -f <filename>` | Replace object with file |
| `oc delete <object type> <object name>` | Delete object from cluster |
| `oc describe <object type> <object name>` | Display object status |
| `oc status` | Display current OpenShift top level project status |
| `oc project` | switch to project, show project |
| `oc new-project` | create new OpenShift project |
| `oc explain <object type>.<field>.<subfield>` | Print out documentation |

---

* Analyse FASTA file with: aragorn?
  * https://github.com/BioContainers/containers/blob/master/aragorn/1.2.38-1-deb/Dockerfile
* https://www.ncbi.nlm.nih.gov/genome/?term=Schizosaccharomyces%20pombe[Organism]&cmd=DetailsSearch
  * ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/002/945/GCF_000002945.1_ASM294v2/GCF_000002945.1_ASM294v2_genomic.fna.gz

* Locally: 

    ```
    $ docker run -v $(pwd):/data/ --rm -it biocontainers/aragorn:v1.2.38-1-deb_cv1 bash
    $ gunzip GCF_000002945.1_ASM294v2_genomic.fna.gz
    $ aragorn GCF_000002945.1_ASM294v2_genomic.fna
    ```

* Run as a pod that doesn't restart 
    * Create persistent volume
    * Create jobs for downloading and unpacking inputdata
    * Create job for running the script
    * Get stdout

* Normally one shouldn't use just any images. But biocontainers.pro are well maintained and curated images aimed at bioinformatics workloads.
* Other good base images
    * The biocontainers images: https://hub.docker.com/u/biocontainers
    * docker.io/alpine: official Docker alpine image
    * https://docs.docker.com/docker-hub/official_images/

---

# OpenShift theory part

1.  Pods are things in OpenShift/Kubernetes that keep track of containers.

    `pod.yaml`:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata: 
      name: simple
    spec:
      containers:
      - name: simple
        image: docker.io/alpine
        command:
        - sh
        - -c
        - tail -f /dev/null
    ```

    * What is different from running directly with docker?
      * No root permissions inside the docker. This would be a huge security risk in multi-tenant container clouds.
        * Not possible to install packages in the "command" section. Not advisable as well.
      * If the command happens to exit or fail, openshift will start the container again. Unless specified differently.
      * The code is run in the rahti cloud instead of your local computer.
    * Remote shell to the running container: `oc rsh simple`
    
    Try `oc status`:

    ```
    In project jkataja-bioweek on server https://rahti.csc.fi:8443

    pod/simple runs docker.io/alpine


    1 info identified, use 'oc status --suggest' to see details.
    ```

1.  We need PersistentVolumeClaim object:

    `pvc.yaml`:

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: yeast-pvc
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
    ```

2.  Simple pod with persistent storage

    `pod.yaml`

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: simple
      labels:
        job: analyze
    spec:
      volumes:
      - name: work-volume
        persistentVolumeClaim:
          claimName: yeast-pvc
      containers:
      - name: read
        image: docker.io/alpine
        command:
        - sh
        - -c
        - tail -f /dev/null
        volumeMounts:
        - mountPath: /data
          name: work-volume
    ```

3.  We need a job that transfers data from ftp://ftp.ncbi.nlm.nih.gov to our volume on rahti

    `transfer.yaml`:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: transfer
      labels:
        job: analyze
    spec:
      restartPolicy: Never
      volumes:
      - name: work-volume
        persistentVolumeClaim:
          claimName: yeast-pvc
      containers:
      - name: transfer
        image: docker.io/alpine
        command:
        - sh
        - -c
        - >
          cd /inputdata &&
          wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/002/945/GCF_000002945.1_ASM294v2/GCF_000002945.1_ASM294v2_genomic.fna.gz &&
          gunzip GCF_000002945.1_ASM294v2_genomic.fna.gz
        volumeMounts:
        - mountPath: /inputdata
          name: work-volume
    ```

4.  Finally, the actual payload job

    * Find image info at: https://hub.docker.com/r/biocontainers/aragorn/tags

    `analyze.yaml`:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: analyze
    spec:
      volumes:
      - name: work-volume
        persistentVolumeClaim: 
          claimName: yeast-pvc
      containers:
      - name: analyze
        image: biocontainers/aragorn:v1.2.38-1-deb_cv1
        command:
        - sh
        - -c
        - >
          aragorn GCF_000002945.1_ASM294v2_genomic.fna
        volumeMounts:
        - mountPath: /data
          name: work-volume
      restartPolicy: Never
    ```

    * Output to `stdout`. Print it with `oc logs analyze`.
```



 
### Log in and create a project

1.  Log in to rahti at https://rahti.csc.fi:8443 with your training account
1.  Authenticate command line session to rahti
    * Click training account name at top right -> Copy login command
1.  Create project named <firstname-lastname>-bioweek
    * Either on the web console *or*
    * on command line using `oc new-project` command
1.  See the output of `oc status`. It should print out the following:

    ```
    In project <firstname-lastname>-bioweek on server https://rahti.csc.fi:8443

    You have no services, deployment configs, or build configs.
    Run 'oc new-app' to create an application.
    ```

# Questions

* Where does rahti pull images? Is this the correct order?
    * internal registry
    * dockerhub
* How to force it to pull eg. `hub.docker.com/biocontainers/aragorn:v1.2.38-1-deb_cv1`
    * `docker.io/biocontainers/aragorn:v1.2.38-1-deb_cv1`
* How big logfile?

