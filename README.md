# olivier

## Explain in your opinion the differences and advantages/disadvantages between:

**Ansible**

* Ansible - agent less, push-based tool and it uses ssh for executing tasks against servers.  So, once a server is provisioned using a .pem key on AWS, it’s  seamless to reply packages.  
* Ansible can inform whether a particular configuration update has failed, allowing user to investigate and fix it.  
* Ansible’s way makes it simple to apply packages, policies on a set group servers (on various environments).
* It can be used to execute commands on a large number of machines, very useful to know server and service status.
* Ansible’s Boto integration makes it useful on AWS.
* Ansible is easier to implement.

**Puppet**
* Agent, push-based tool.  It’s been around for longer and has wider set of usage in the industry.
* A newly provisioned server contacts a central server  (puppet master) and gets updated as per configuration.  
* Puppet will periodically pull resource definitions and update the server.
* It’s reposting capability makes it very useful to know status of servers.

**Framework of your choice**

Ansible - It’s simple and it works. The main reason, there are lots more important things to do than simply worry about the choice of CM tool.

## Design a CI/CD pipeline from repository to production, high level

* Repository created in Github/BitBucket
* Artifacts/Build Job created in Jenkins. Web Hook is configured to automate build for each push.
* Downstream Jobs are created to deploy package to all environments (ex: dev, staging and prod). A single Artifact is copied to all environments.
* A unit Test Job is created and run after Dev env deployment.
* On every environment deployment, an smoke test is carried out after Artifact is deployed and service is restarted.
* If a Load balancer is used for proxy, every server is taken off the LB before package deployed and brought back in once the smoke is successful.

## How would you track a REST request in a distributed architecture?

It's common to do something like add a "request-id" http header at the "edge" and have every service forward+log that id for any work/transaction it does relating to that request.
There are also framework like finnagle and zipkin and open-tracing which can sort of help with it, but nothing out of the box.

## List all the orchestration frameworks you know or heard of and explain what problems they solve and how

**Mesos**

Apache Mesos is an open source cluster manager that simplifies running applications on a scalable cluster of servers, and is the heart of the Mesosphere system.

Mesos offers many of the features that you would expect from a cluster manager, such as:

* Scalability - Scalability to over 10,000 nodes.
* Resource isolation for tasks through Linux Containers.
* Scheduler Service - Efficient CPU and memory-aware resource scheduling.
* Uses Apache ZooKeeper for Service Availability.

**Kubernetes**

According to the Kubernetes.io, "Kubernetes is an open-source platform for automating deployment, scaling, and operations of application containers across clusters of hosts, providing container-centric infrastructure."

Kubernetes can be implemented on any platform: public, private, hybrid cloud or on Data Centres. It is a Container Orchestration tool.

**Swarm**

Docker Swarm is native clustering for Docker. It turns a pool of Docker hosts into a single, virtual host.

**Framework of your choice**

At this stage, there isn't a clear winner for me. It all depends on my requirement, platform and ease of deployment. Having said that, I prefer Kubernetes as I find it's

Order the following from the slowest to the fastest operation

1. CPU register access
2. Memory access
3. Context switch
4. Disk access
 
List commands for the following common tasks:

1. Resource issue diagnostics <br>
top, htop, free, iostat, vmstat, ps, sar

2. IO and IO/wait related issues<br>
iostat, iowait, iotop.

3. Networking and Packet loss<br>
`$ netstat -s | egrep -i 'loss|retran'`


**In your words - What is DevOps?**

In DevOps, Ops and Devs work together with a common goal of bringing new features to product line through collaboration, understanding and sharing knowledge together. DevOps a practice, it's something you do. It's not a role, nor a team.  

**What are MicroServices?**

Though I am instructed not to copy/paste, I find that the definition here http://www.brunton-spall.co.uk/post/2014/05/21/what-is-a-microservice-and-why-does-it-matter/ is closer to what I think a good explanation. MicroServices pattern aims to solve problems by keeping following ideals

* A small problem domain
* Built and deployed by itself
* Runs in its own process
* Integrates via well-known interfaces
* Owns its own data storage

## Exercises

Generate 100 files with random data

    1. Every 5th file should contain "Nothing to see here".
    2. Every 11th file should contain the contents of all previous files.
    3. Random data files should not exceed 512 characters in text.
    4. You should implement tests.

Write an Ansible/Puppet/Something module that
* Handles NTP on a large network, both server and clients

Write a Dockerfile for Redis
    1. That accepts port configuration from ENV variables
    2. That accepts memory limit configuration from ENV variables
