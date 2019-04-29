# Google Cloud Marketplace (formally Launcher)fLyMd-mAkEr

quickly deploy functional software packages on GCP

most at no additional charge beyond normal charges

will update base images for software packs to fix critical issues and vulnerabilities, but not software

### demonstration

- click cload launcher
- in search bar type LAMP (envs for web develppment)
- estimates providerd, click laundch on compute engine, use defaults
- click deploy

- login using ssh 
- cd to dir
- copy php test page
- end ssh
- confirm php test page


## Qwik labs

get hands on experience

- log into coursera in incognito window
- go to lab activity page
- open tool button
- click start lab
- t 

# Policy Hierarchy

## IAM (Cloud Identity and Access Management)

manage access control by defining who(identy) has what access(role) for which resource

grant only necessary acess to your resources
  - security principle of least privilege
  
 #### identities:
 
- google account: specific person

- service account: belongs to app instead of indiv end user, can create as many as needed
- google group: named collection of google accounts and service accounts
   - has unique email address
   - convenient way to apply access polity to collection of users
   - easily add/remove users
- g-suite domain: all google accounts created in orgs G Suite account
- cloud identity domain: like g-suite but users w/o g-suite apps and feature
- allAuthenticatedUsers: anyone who is authenticated w. google account or service account
- allUsers: anyone on internet
 
 #### Resource
 
 You can grant access to users for a GCP resource. Some examples of resources are projects, Compute Engine instances, and Cloud Storage buckets.
 
 #### Permissions
 
- determine what operations are allowed on a resource. 
- In the Cloud IAM world, permissions are represented in the form of 
    - `<service>.<resource>.<verb>`
    - ex: `pubsub.subscriptions.consume` 
 
 - You don't assign permissions to users directly. Instead, you assign them a Role which contains one or more permissions.
 
 #### Roles
 
- collection of permissions
- cannot assign a permission to the user directly; instead you grant them a role. 
- When you grant a role to a user, you grant them all the permissions that the role contains.
- types of roles:
  - Primitive roles: The roles historically available in the Google Cloud Platform Console will continue to work. These are the Owner, Editor, and Viewer roles.
  - Predefined roles: Predefined roles are the Cloud IAM roles that give finer-grained access control than the primitive roles. 
    - For example, the predefined role Pub/Sub Publisher (roles.pubsub.publisher) provides access to only publish messages to a Cloud Pub/Sub topic.
  - Custom roles: Roles that you create to tailor permissions to the needs of your organization when predefined roles don't meet your needs.
  
# google compute Engine
- create and run vms on google infrastuctre. 
- create vm on GCP console / gcloud command line tool
- 2 kinds of persistant storage
    - standard
    - ssd
- can include local SSD but doenst keep data after vm terminated
- can pass startup scripts
- autoscaling  lets you add and take away VMs from app based on load metrics.
- supports diferent kinds of load balancing

###### preemptible VM
- terminates if resources are needed elsewhere, job should be able to stopped and restarted


  
## Virtual Private Cloud (VPC) Network
- connect GCP resoureces to each other and to the internet
- segment, firewals rules, create static routes to forward traffic
- have global scope
- define own network layout with global scope
- VPC subnets can span zones that make up a region (can incorporate fault tolerance w/o complicating net topology)
- resources in different zones on same subnet.
- increase size of a subnet in custom net by expanding range of ip addresses. doesnt affect already configured VMs 
  
#### important capabilities
- have routing tables
  - forward traffic from one instance to another in same network (across sub-networks / GCP zones, ect)
- router table built in: dont have to manage router/firewall
  - restrict incoming/outgoing traffic
- can define firewall rules on metadata tables
- VPC peering to to establish relationship between multiple VPCs
- shared VPC for full power of IAM control
 
###### Cloud Load Balancing
- fully distributed software defined managed service for all traffic
- can put in front of all traffic (hhtp, https, tcp, ssl, udp)
- reacts quickly to changes in users, traffic, backend health, network conditions, ect
 
 
###### cloud DNS
- publish and manage millions of DNS zones and records
- use via GCP console, the command line interface or the API
 
###### cloud CDN
- system of edge caches. You can use this system to accelerate content delivery in your application using Google Cloud CDN. 
  
###### Cloud router 
- lets your other networks and your Google VPC exchange route information over the VPN using the Border Gateway Protocol.

# Cloud Storage

### cloud storage
- cloud storage is often the ingestion point for data being moved into the cloud and is frequently the long term storage location for data.
- object storage, not filesystem
- not managed as blocks on disk
-data stored in key/value pairs
  - key is often urls
- capacity not provisioned ahead of time
- used for (web content, disaster recovery, distibuting large data objects via direct download)
- comprised of buckets
- storage objects inmutable
- encrypted server side before written to disk, data in transit encrypted w/ https
- bucket given globally unique name at creation
- choose where and storage class
- IAM for broad user control
- can use Access Control Lists (ACL) for fine tuning user control
  - define who has access to buckets and objects as well as what level of access they have
  - consist of 2 peices
    - who can do what
- can turn on object versioning
- life-cycle management policies (ex: tell cloud starage to delete objects older than 365 days)
- cost per gb pricing
- egress/data transfer charges may apply
- to tranfer data:
  - GSutil:
  - drag and drop in GCP console
  - storage transfer storage for batch transfers
    - rackable, high capacaity storage server, securly transfer up to petabyte of data
    - still in beta not available everywhere
  - import/export bigquery and cloud sql 
 
 ###### storage classes
- regional
   - high performance
   - stored in specific GCP region
   - cheaper than multi-regional
   - store data close to compute machine, vm, or kubernetes engine clusters
   - better performance data intensive comps
   - in region analytics/transcoding
- multi-regional
   - high performance
   - geo-redundant
   - stored in atleast two geographic locations separated by > 160km
   - for frequently accessed data 
- nearline
   - backup/archival
   - low cost, highly durable
   - infrequently accessed, read/write less than 1/mo
   - access for per gb fee
- coldline
   - backup/archival
   - very low cost highly durable
   - for data archiving, online backup, disaster recover
   - accessed less than 1/year
   - slightly lower availability, 90 day min store dur, costs for data access, higher op costs


### cloud SQL
- relational database
- mysql or postgresql (beta) as fully managed service
- provides
    - provide several replica services like read, failover, external replicas
    - helps backup data with on-demand or scheduled backups
    - scales vertically by changing machine type
    - scales horizontally via read replicas
- include network firewalls, customer data is encrypted on googles internal nets, stored in db tables, temp files and backups
- accessible by other GCP services and external services

### Cloud Spanner
- like cloud sql, but scales horizantilly,
- offers transactional consistency at global scale, schemas, sql and automatic synchronous replication for high availability
- use if outgrow any relational database, or sharding db for throughput high perormance, need transactional consistency, global data and strong consistance, consolodate db
- natural use cases include financial apps, and inventory apps

### Cloud Data Store
- NoSQLm store structured data from app engine apps,
- can also build solutions that span app engine and compute engine with cloud datastore as integration point
- auto handles sharding and replication, highly avaiable and durable db that scales
- offers transactions that affect multiple db rows, can do SQL like queries

### Cloud Google Big Table
- NoSQL, big data database
- all rows don't need same columns
- sparsley populated tables that can scale to billions of rows and thousands of columns
- GCP manages surface, dont need to configure and tune it
- ideal for data w/ single lookup key
- large amounts of data, low latency
- offered through opensource API HBase (native database for apache hadoop project)
- scalable
- handles admin tasks like upgrades and restarts transparently
- encrypts in flight and at rest
- IAM permissions to control who has access
- can interact with other GCP services and third party clients


# Containers, Kubernetes & kernetes Engine
- containers and kubernetes engine between compute engine and networking, benefits of both
- Infrastructure as a Service allows you to share compute resources with other developers by virtualizing the hardware using virtual machine
- idea of a container is to give you the independent scalability of workloads, and an abstraction layer of the OS and hardware
- on each host, need os kernel that supports containers and container runtime
- Kubernetes makes it easy to orchestrate many containers on many hosts, scale them as microservices, and deploy rollouts and rollbacks
- Kubernetes is an open source orchestrator that abstracts containers at a higher level so you can better manage and scale your applications
 
 
### kubernetes
- set of APIs that you can use to deploy containers on a set of nodes called a cluster
- divided into a set of master components that run as a control plane, and a set of nodes that run containers
- node represents a computing instance like a machine
- Google Cloud, nodes are virtual machines running in Compute Engine. You can describe a set of applications and how they should interact with each other, and Kubernetes figures how to make that happen
- can bootstrap Kubernetes using Kubernetes Engine, or GKE. GKE is hosted Kubernetes by Google. GKE clusters can be customized, they can support different machine types, numbers of nodes, and network setting
- you deploy containers on nodes using a wrapper around one or more containers called a pod. A pod is the smallest unit in Kubernetes that you create or deploy. A pod represents a running process on your cluster as either a component of your application, or an entire app
- pod provides a unique network IP, and setup pods for your containers, and options that govern how a container should run
- By default, pods into deployment are only accessible inside your GKE cluster. 
    - To make them publicly available, you can connect a LoadBalancer to your deployment by running the kubectl exposed command
- You could also use auto scaling with all kinds of parameters
- to rollout new code, use kubectl rollout, change config file and apply the changes using kubectl apply, new pods created according to update stategy.

   
# app Engine (PaaS)
- dont have to worry about infrastructure, only code
- includes: 
    - NoSQL database, 
    - in-memory caching, 
    - load balancing, 
    - health checks, 
    - logging
    - way to authenticate users
- scales app automatically, only pay for resources you use
- no servers to provision/maintain

### environments
- can be tested locally with app engine software dev kits
- SKDs provide simple commands deployment

###### standard
- free daily usage quota for use of some services
- simpler, fine grained auto-scaling
- low utilization apps might be able to run at no charge
- provides runtimes and libraries for java python PHP Go
- include libraries that support app engine APIS
- enforces restictions on code by making it run in sandbox
  - cant write to local filesystem
  - has to write to db service instead if data persistent
  - 60 sec timeout on all requests
  - cant install arbitrary third party software

###### flexible
- can specify container app engine runs on
- code in other languages
- lets you ssh into machines that run app
- use local disk for scratch base
- install 3rd party software
- apps make calls to network w/o going through app engine
- control geographic region where they run

# Cloud endpoints
- easily expose api
- ensure only consumed by trusted developers
- easily monitor and log use
- single coherent way to know which end user is making call
- support apps running in GCPs compute platforms

# apigee Edge
- for developing and managing api proxies
- focuses on business probs like rate limiting, quotas, and analytics
- many users providing software services to other companies

# Development in the Cloud

### Cloud Source Repositories
- keep code private to a GCP project
- use IAM permissions
- unlimited git repos
- source viewer to browse and view

#### Cloud Functions
- automatically run func when necessary
- no worry about servers/runtime binaries
- pay whenever functions run in 100 millisecond intervals
- can trigger on events in cloud storage, Could Pub/Sub or in HTTP call
- run w/ JS or Node.js

#### Deployment Manager
- set up deployment template (declarative rather than imperative)
- infrastucture management service, automates creation/management of GCPresources
- template made w/ YAML or Python
- template goes to deployment manager, which creates environment
- can later edit template and have deployment manager update env
- template can be stored and VCed in cloud source repo

#### Stackdriver
- tool for monitoring, logging & diagnostics
- access to signals from infrsturcture platforms,vms, containers, middleware, and application tier, logs, metrics, and traces
- insight into apps health, performance, availability
- core components
  - monitoring
    - checks endpoints of service
    - config uptime checks associated w/ urls, groups, or resources (instances, load balancers)
    - set alerts on criteria
    - uptime/health checks
    - use with popular notification tools
    - configure dashboards
  - logging
    - platform, system, app logs
    - view/filter/search/export logs
    - log-based metrics --> incorporate into dashboards and alerts
    - export logs to BigQuery, Cloud Storage, & Cloud PubSub
  - trace
    - sample latency of app engine apps
    - report per-url stats
  - error reporting
    - tracks and groups errors
    - notifies when new errors are detected
  - debugging
    - connects app production data to source code
    - inspect stat of app at any code location in prod
    - view app stage w/o adding logging statements
    - works best when source code available such as in cloud source repos
    
# Big Data / Machine Learning
- integrated serverless platform
  - no worry about provisioning compute instances to run jobs
  - services fully managed
  - only pay for used resources
  - integrated (GCP data services work together to create custom solutions)

### Big Data
#### Cloud Dataproc
- run hadoop, spark, hive and pig on GCP
- request hadoop cluter
- built in <90secs on compute engince VMs 
- scalable
- default hadoop software config or customiz
- stackdriver monitoring
- can use preemptive instances for batch processing to save money
- datamining w/ spark / spark SQL
- machine learning w/ MLib 

#### Cloud Dataflow
- stream, and batch processing; unified and simplified pipelines
- build data pipelines; work for batch/streaming data
- automates management of processing resources requirements
- expressive pipelines, elastically scaled
- dynamically re-balance lagging work
- useful for fraud detection, financial services, IoT analytics, healthcare, logistics, click stream, PoS, segmentation analysis in retail
- useful in real time apps like personalizing gaming user experiences

#### BigQuery
- analytics database; stream data at 100,000 rows/sec
- large scale, low cost, analytics data warehouse
- no infrastructure management
- use SQL
- load data from cloud staorage / stream at up to 100,000 rows/s
- read/write via cloud dataflow, hadoop, spark
- free montly quoteas, seamless scale
- available 99.9% service level agreement
- specifiy region data kept
- pay for storage seperate from queries
- control who has access to data, share datasets (they pay for their own queries)
- long term storage pricing is auto discount for data residing in Big Query for extended periods of time
  - price drops after 90 days

#### Cloud Pub/Sub
- scalable & flexible enterprise messaging
- let independent apps send / receive messages
- pub -> publish, sub -> subscibe
- => 1 subs can recieve messages
- receiving messages not neccessarily synchronous
- good for decoupling systems (systems dont have to scale together)
- on demand scalability to >1mil messages/sec, you choose quota
- good when data arrives and high and unpredictables rates (IoT devices/services)
- works well with dataflow, GCP compute platforms

#### Cloud Datalab
- interactive data exploration
- ready to use python environment (like Jupyter notebooks)
- runs in compute engine VM
- only pay for used resources
- integrated with BigQuery, Compute Engine, Cloud Storage
- visualize data w/ google charts / matplotlib
- learn from published notebooks

### Cloud Machine Learning
- provides modern machine learning services w/ pre-trained models
- platform to generate own tailored models
- range of APIs
- 2 main uses:
  - structured
    - classification / regression
   - unstructured:
     - image/video/text analytics

##### tensorflow
- GCP makes tensor processing units (TPUs) available -> fast processing

##### google machine learning engine
- easily build machine learning models
- any type/size of dataperform large scale training 

#### APIs

##### cloud vision
- analyze images w/ simple rest API
  - logo detection, label detection, etc
- classification, object detection
##### NLP
- audio, text
- language recognition/translation
  - 80 language variants
##### cloud video intelligence
- annotate videos, identify key entities (nouns, where in video they occur)
- in beta



