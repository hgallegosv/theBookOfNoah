# Todos
  -
# links
  - [lynda GCP essential training](https://www.lynda.com/Google-Cloud-Platform-tutorials/Google-Cloud-Platform-Essential-Training/540539-2.html)
  - [gcloud architect exam guide](https://cloud.google.com/certification/guides/cloud-architect/)
  - [coursera GCP fundamentals](https://www.coursera.org/learn/gcp-fundamentals)
  - [links for transform based programming model](https://scholar.google.com/scholar?q=transform+based+programming+model&hl=en&as_sdt=0&as_vis=1&oi=scholart)
  - [stream analytics](http://www.dataversity.net/streaming-analytics-101/)
  - [project jupyter: the jupyter notebook](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html)
  - [martin fowler serverless architectures](https://martinfowler.com/articles/serverless.html)
  - [nosql wide column store](https://www.forbes.com/sites/metabrown/2018/03/31/get-the-basics-on-nosql-databases-wide-column-store-databases/#453e9a4b6e50)
  - [types of relational and nosql dbs](https://www.forbes.com/sites/metabrown/2018/03/31/get-to-know-relational-and-nosql-databases-that-power-big-data-analytics/#725169291943)
  - [Google Cloud: Application Development Coursera Course](https://www.coursera.org/learn/getting-started-app-development/home/welcome)
  - [the worker pattern](https://gist.github.com/ryandotsmith/1660752)
  - [user auth/password management](https://cloud.google.com/blog/products/gcp/12-best-practices-for-user-account)
  - [google cloud client libraries](https://cloud.google.com/apis/docs/cloud-client-libraries)

# Terms
  - cloud computing:
    - on demand self service: no human intervention to get resources
    - broad network access from anywhere
    - resource pooling: provider shares resources to customers
    - rapid elasticity: if you need more resources you can get more or if you need less you can reduce usage
    - measured service: pay only for what you use
  - virtualization: managing services separately from the hardware
  - GCP Computing Architectures
    - IaaS: infrastructure as a service
      - provide raw, compute, storage, and network
      - you pay for what you allocate
      - e.g. compute engine
    - Hybrid: incorporating aspects of Iaas and PaaS
      - e.g. Kubernetes
    - PaaS: platform as a service
      - bind application code you write to libraries that give access to infrastructure your application needs
      - you pay for what you use
      - e.g. app engine
    - SaaS: Software as a Service
      - applications consumed directly over the internet by end users
      - e.g. gmail
  - git: used to store and manage their source code trees whether on-premise or hosted
  - serverless:
    - applications that significantly or fully incorporate third party, cloud-hosted applications and services to manage server-side logic and state
    - applications where server-side logic is written by the application developer, but run in stateless compute containers that are event-triggered, ephemeral and fully managed by a third party
    - you dont have to provision compute instances to run your jobs
  - integrated platform: products on the platform can seamlessly commmunicate with eachother
  - stream analytics: stream processing analyzes and performs actions on real-time data through the use of continuous queries
    - connects to external data sources, enabling applications to integrate certain data into th eapplication flow, or to update an external database with processed information
  - pub/sub model:
    - pub: the publisher who posts messages to specific topics
    - sub: the subscriber who listens for messages about specific topics
    - push vs pull
      - push: subscribers are pushed messages when they arrive
      - pull: subscribes poll/check for new messages at arbitrary intervals
  - metadata: information that describes data
  - database architectures
    - relational:
      - use metadata to provide information about the data source, data collection methods, and meaning
      - tabular structure keeps data well organized and accessible
      - exact kind and quanitity of data is always known
    - NoSQL
      - dont use normalized data model found in dbs,
        - dont organize data in tables, rows and columns
      - use cases
        - data has little/inconsistent structure
        - data must be distributed across more than one emachine
        - speed is more important than accuracy
        - application requires data types or analysis methods that common relational dbs handle poorly
      - types
        - content store: aka content repository: large, complex data formats like video, audio
        - document store: semi-structure data like registration forms, business correspondence, articles
        - event store: tracking events in real time
        - graph: finding connections among people and things
        - key value: associative array, data structure, dictionary, hash,
          - simple structure,
          - flexibility
          - scalability
        - multivalue: NF2, non-first normal form systems
          - complex data structures with schemas similar to relational dbs
        - navigational: hierarchical (one to many) or network (many to many) data structure
        - object oriented: model data as objects, similar to OOP
        - RDF store: resource description fraemwork, semantic graph dbs, or triple stores
          - information processing in applications that connect multiple data sources
        - search engine: finding information in documents
        - time series: time series data
        - wide column storea: manage data that wont fit on one computer; aka column families, columnar databases, column-oriented DBS
          - columns: related facts
          - column families: groups of columns that have content and function similar to tables in a relational database
        - XML: native XML db or native XML dbms
          - data in xml format or varied copmlex formats like audio or video
  - setting up your environment
    - imperative approach: figure out the commands you need to setup/change from the old state to the new
    - declarative: use a template to specify what the environment should look like


# Best Practices
  - Cloud Native Application Goals
    - global reach and can handle high traffic volumes reliably
    - scalability
    - high availability
    - security
    - loosely coupled
    - resiliency
    - repeatable & rollbackable deployments
    - build and release systems that enable continuous integration and delivery
    - debugging, monitoring and performance-tuning are crucial for running robust applications
  - understand your data storage needs to and storage options
    - storage needs
      - high volumes of flat structured data
      - relational data
      - multimedia
  - interleaved ttable: a table that you declare to be a child of another table you want the rows of the child table to be physically stored together with the associated parent row


## app code and environment
  - code repository
    - all code should be stored in a repository
    - enables you to track changes and setup systems for continuous integration and delivery
  - use a dependency manager
    - this allows you to never store external packages in your repository
    - each version of your application should explicity list its dependencies
  - configuration settings
    - separate config settings from coder
    - never store config settings as constants
    - specify config settings as env variables
      - allows you to easily modify settings in differeent environments


## Microservices Architecture
  - enables you to structure your application in relation to your business boundaries
  - designed for loosely coupled services
    - this makes them resiliant to spikes, failures, and changes to traffic (load)
    - use pub/sub model
      - a cloud pub/sub topic can be the message queue
        - enabling perform asynchronous processing, and buffer requests during spikes in traffic
    - consumers of HTTP apis should bind loosely with publisher payloads
      - never attempt to bind with all fields in the payload
      - this enables the publisher to modify the API in a backwards compatibld manner
  - implement stateless components for scalability
    - never store state internally or access shared state
      - shared states are a common bottleneck for scalability
    - each component should focus on compute tasks only
      - enables you to implement the worker pattern in order to add/remove additional instances of the component for scalability
    - components should startup & shutdown quickly to enable efficient scaling
  - cache application data/content
    - improves performance and lowers network latency
    - anything that is computationally intensive to calculate
    - anything that is frequently accessed
    - never cache private/personal data
    - always follow modern cache strategies
    - store data in a cache service like memcached/redis
    - store webpages/static content in a CDN
  - each service is monitored and can fail gracely on error
  - each service lives as a distinct application that can be updated, deployed and scaled indepdendently of each other
    - perfect for handling feature changes and bug fixes
  - far more easier to understand where code needs to be changed compared to a monolithic application
  - each service has distinct dependencies (vs the tangled dependencies in large monoliths)
  - things to watch out for
    - remote operations can be unpredictable and response times can make your app seem slow
      - keep ui responsive
      - always perform backend operations asynchronously
      - keep operations on the user thread at a minimum
      - use event-driven processing where possible
  -


## API Gateways
  - enables backend functionality to be available to consumer applications
  - if your backend cannot be moved to the cloud
    - the API can still serve as a facade or adapter link instead of communicating with the legacy backend using outdated protocols or desparate interfaces
      - each consumer can then invoke a modern cloud API which then invokes the legacy backend

## External User Administration
  - use federated identity management
    - minimizes effort for user administration
  - whether using FIM or building inhouse, always:
    - implement secure solution for authenticating & authorizing users
    - use strong cryptographic hash for passwords
    - allow for third party identity providers
    - separate the concept of user identity and user account
      - users are not an email address, phone number, etc.
      - users are a columnation of their unique personalized data and experience within your service
    - maintain low coupling and high cohesion between different parts of a user's profile
    - allow multiple identities to link to a single user account
    - don't block long/complex passwords
    - don't impose unreasonable ruules for usernames
    - allow users to change their username
    - permit users to delete their accounts
    - make a consious decision on session length
    - use 2-step verification
    - make user IDs case insensitive
    - build a secure auth system

## Application Reliability
### health-check endpoints
  - monitor the status of your app and services via a Health Monitoring Agent (e.g. a load balancer)
    - periodically sends requests tot he health check endpoint
  - ensure they are available and performing optimally
  - setup alerts to devOps at thresholds
  - the health-check handler should check the health of:
    - all critical dependencies
      - storage
      - database
      - network connections
      - etc
    - all infrastructure components required for the service to function properly

### Logging
  - monitoring your app's performance
    - debugging
    - error reporting
    - tracing
    - logs-based metrics
    - monitoring
  - treat your logs as event streams: logs constitute a continous stream of events that keep occuring as long as the app is running
  - never manage your log files in your application
    - write to an event stream, e.g. standard out and let the underlying infrastructure collate all events for later analysis and storage
  - setup logs-baased metrics and trace requests across different services in you rapplication

### error handling
  - handle transient and long-lasting errors gracefully
  - transient errors: retry with exponential backoff
  - service availability errors: implement a circuit breaker
  - each UI component should degrade gracefully
  - for errors that propagate back to the user
    - consider degrading the application gracefully instead of explicity displaying the error message
      - this can help with security

### Testing
  - setup high availability tests
  - setup functional tests
  - setup performance tests
  - setup tabletop tests
    - teams discuss how they will respond in failure scenarios but dont perform any real actions
  - setup canary testing
  - identify failure scenarios and simulate them in your development environment to test the efficacy of your disaster recovery plans
    - connectivity failiure
    - on-premises data center / other cloud provider failure
    - zone/region failure
    - deployment rollback
    - data corruption caused by network / application issues
  - develop disaster recovery plans
    - people are notified
    - traffic is rerouted using redundant routes
    - make sure data was not corrupted during failure & recovery process
    - ensure all services/processes are restored ina timely manner
    - processes
    - tools

## DevOps
  - devops model
    - should be fullly automated
    - continouosly integrated
    - continuously deployed
  - code repo -> build system -> deploy system ->
    - test environments: execute integration, security, and performance tests
    - production environment: monitor performance with metrics and alerts
  - integrate and deliver small changes vs big changes
    - lowers risk of regression
    - debug issues faster
    - rollback to the last stable build


### SecDevOps
  - consider security throughout the continuous integration and delivery process
  - automate security checks
    - confirm your using the most secure version of third party dependencies
    - scan code for security vulnerabilities
    - confirm resources have permissions based on principle of least privilege
    - detecting errors in production


## Application Security
### Data
  - data sovereignty
    - some regions and industry segments have strict compliance requirements for data protection and consu mer privacy
    - Areas to consider
      - processing user data
      - storing user data
      - sharing user data
      - review the industry segment and region where your users live and your services will be located


## Migrating to the cloud
  - implement the strangler pattern: incremently replace components of the old application with new services
    -

# GCP PRODUCTS
## development
### cloud source repositories (i.e. git)
    - keep code private to a GCP project
    - IAM permissions used to protect the code
    - fully featured git repositories
    - source viewer: browser and view repo files within the GCP console
    - allow external users
  - supported platforms


### cloud functions
    - create single-purpose functions that respond to events without a server/runtime
    - written in javascript, execute in managed node.js environment on GCP
    - triggers
      - you choose what events you care about
      - you attach javascript functions to your event triggers
      - supported platforms
        - cloud storage events
        - cloud pub/sub events
        - http calls
    - use cases
      - breakapart an existing monolithic application into microservices with little developer effort
      - enhance existing applications without having to worry about scaling
      - enhance an event-driven application without having to provision additional compute resources
    - cost
      - pay when function runs in 100ms intervals

## deployment
### deployment manager
  - infrastructure as code
  - automates the creation and management of your GCP resources via templates
  - you can version control your templates in cloud source repos
  - workflow
    - create a template file in YAML/Python that describes what you want the components of your environment to look like
    - deployment manager executes your template to create the environment described
    - to make changes, edit the template and deployment manager will update your environment automatically
    -

## monitoring
  - you cant run an application stably without monitoring
  - use cases
    - understanding if the changes made good / bad ?
    - respond with information vs panic when end-users complain
### Stackdriver
  - insight into your applications health, performance and availability, diagnostics, and various other metrics
  - gives you access to many signals:
    - infrastructure platforms
    - virtual machines
    - containers
    - middleware
    - application tier
  - core components
    - monitoring: checks the endpoints of applications and other internet accessible services running in GCP
      - platform, system and application metrics
      - uptime/health checks: associated with URLS, groups, or resources
      - alerts: on any criteria/condition and integration with popular notification tools
      - dashboards: visualize state of app
    - logging: view logs from applications
      - define metrics based on log content
      - export to bigquery, cloud storage, and cloud pubsub
      - platform, system, and application logs
      - log search, view, filter, and export
    - error reporting: tracks and groups errors in cloud applications and notifies you when new errors are detected
      - error notifications
      - error dashboard
    - debugging: connects your application's production data to your source code for you to inspect the state of your app at any code location in production
      - view the app state without adding logging statements
      - works best when your app source code is available
        - cloud source repos
        - other repos
    - Trace: sample the latency of app engine applications and report per-url statistics
      - latency reporting and sampling
      - per-url latency and statistics
  -

# GCP Platform Administration
  - principal of least privilege: users only receive permissions to do what they are required to do

## Managing resources
### Web Console:
  - web based admin
    - view and manage projects and their resources
    - enable and disable and explore API of GCP resources
  - API Explorer: testing google cloud APIs in a sandbox
#### Cloud Shell:
  - CLI to access GCP resources from your browser
    - built-in authorization to cloud platofrm console proejcts and resources
    -
  - a temp VM instance
    - 5gb of persistent disk
    - pre-intsalled google cloud sdk
  - features
    - web preview: start a web browser on an arbitrary port to the connected resource
    - built-in code editor
### Google Cloud SDK:
  - manage resources and applications, is available as a docker image
    - useful for writing scripts
  - has 3 tools
    - gcloud: all services except cloud storage and bq
      - perform common tasks on GCP
      - create and manage GCP resources
      - script/automate gcloud commands
      - use gcloud interactive shell
    - gsutil: for cloud storage
      - create and manage buckets
      - upload, download and delete objects
      - move, copy and rename objects
      - manage access to stored objects
    - bq: BigQuery
      - manage datasets, tables, and other BigQuery entities
      - allows you to run queries

### Google API client library:
  - should only be used if your programming language does not have a a Google Client Library
    - does not support gRPC
    - use JSON as an interchange format
    - uses OAuth 2.0 for authentication and authorization
    - each API is enabled through console
    - include daily quotas and rates that can be raised by request
    - API Explorer: interactive tool to easily try google APIs using a browser
      - see Docs
      - execute requests for any method and see responses in real time
      - make authenticated and authorized API calls


### Cloud Client Libraries:
  - API Client libraries: open source generated supporting various languages
    - handle low level communication with the server, including authentication with google
    - installed using familiar package managers
    - provide retry login for failed requests automatically
    - gRPC: google remote procedure call APIs
      - makes it easier to build connected systems by enabling client and server applications to communicate transparently
      - makes it
  - recommended method to invoke google cloud API
  - architecture
    - every package uses a client as a base for interacting with an API
      - authentication
        - if your app is on app/compute engine authentication will just work
        - if you dont explicitly provide credentials, the client will reuse the credentials from the gcloud tool if it has already been setup
        -
### firebase sdk:
  - firebase: mobile and web app dev platform
    - ios, android, web, c++, unity, nodejs
  - use cases
    - implement federated identity management with firebase authentication
    - firebase sdk for cloud storage stores files directly in google cloud storage buckets
    - use app engine api to share data between firebase and app engine
    - cloud functions for firebase lets you run backend code in respond to events triggered by firebase features and http requests
    -
### Mobile App
    - manage virtual machines and DB instances
    - manage apps in google app engine
    - manage billing
    - visualize projects via customizable dashboards

## GCP Regions and Zones
  - Zone: deployment area for GCP resources like a VM in Compute Engine
    - you generally spread resources across multiple zones in a region to build a fault tolerant application to protect against unexpected failures
    - e.g. europe-west2-a
  - Regions: independent geographic areas
    - all zones in tbe same region have fast network latencies under 5 ms
    - Multi-region: storing your data in multiple regions for redundancy

## resource hierarchy:
  - policies can be defined at each level
  - policies are inherited downward
    1. org node: the top node that allows you to have visibility into all of your folders and projects
    2. folders: groups projects into logical units
    3. projects: organize your resources, and group resources that have a common business objective
      - all GCP resources belong to a project
      - are the basis for enabling and using GCP services like APIs, billing, collaborates, etc
      - each project is a separate compartment
      - billed separately and managed separately
      - identifying a project
        - ID: immutable & globally unique and chosen by you
        - name: mutable & chosen by you
        - number: immutable globally unique and chosen by GCP
    4. resources: e.g. storage, VM
      - inherit policies of their parent resource
      - parent policies cant take away access thats granted at a lower level

## IAM: Cloud Identity and Access Management
  - IAM: controls WHO can take WHAT action on specific Resources
### IAM Users: The WHO
  - types of users
    - a google account or cloud identity users e.g. blah@gmail.com
    - a google group e.g. test@googlegroups.com
    - a G suite domain or cloud identity domain  e.g. blah.com
    - a google service account: provision an ID to control server-to-server interactions in a project
  - use cases:
    - control privileges used by resources for applications to perform actions on behalf of authenticated end users
    - authenticate one service to another
    - control privileges used by resources
  - authentication:
    - use cryptographic keys
    - can be assigned custom or predefine roles
  - identified by an email address
    - PROJECT_NUMBER-compute@developer.gserviceaccount.com
    - PROJECT_ID@appspot.gserviceaccount.com


### IAM roles: the WHAT
  - role: a collection of permissions
  - types of roles
    - primitive role: apply across all GCP services in a project
      - owner: invite, remove, delete,
        - includes editor + viewer permissions
      - editor: deploy apps, modify code, configure services\
        - includes viewer permissions
      - viewer: read only access
      - billing admin: manage billing, add & remove admins
    - predefined roles: IAM fine-grained permissions tailored for specific services
    - custom roles: define a role with a specific set of permissions to help implement a principal of least for projects and organizations
      - cant be used for folders

## Security
 - customer responsibility
   - content
   - access policies
   - usage
   - deployment
   - web app security
   - identity
 - google responsibility
   - operations
   - access and auth
   - network security
   - os, data and content
   - audit logging
   - network
   - storage and encryption
   - hardware
 - levels
  - operational security: intrusion detection systems; techniques to reduce insider risk; employee U2F use;
  - internet communication: Google Front End service; designed-in denial of service protection
  - storage services: encryption at rest;
  - user identity: centrial identity service with support for U2F;
  - service deployment; encryption of inter-service communication;
  - hardwaare infrastructure; hardware design and provenance; secure boot stack; premises security
  - googles infrastructure provides cryptographic privacy and integrity for remote procedures called data-on-the-network, which is how google services communicate with each other
    - automatically encrypts PC traffic in transit between data centers
    - GFE: the google front end:

# Core Products

## Cloud Launcher
  - tool for quickly deploying functional software packages to GCP
    - marketplace containing prepackaged ready to deploy solutions
    - some created by google (free), other by third party vendors (could cost)
    -

## Virtual Private Cloud
  - generally the first step is to define a VPC for a project
  - connects GCP rsources to each other and the internet
  - VPC Peering: interconnect networks in GCP projects
  - shared VPC:  share a network or individual subnets with other GCP projects
  - Characteristics
    - networks are global
    - subnets are regional
      - different zones can be part of the same subnet
      - can dynamically increase the size of a subnet by expanding the ranges of IPs allocated to it
    - routing tables: used to forward traffic from one instance to another within the same network without requiring an external IP address
    - firewall: are globally distributed, you can restrict access to instances both incoming and outging traffic
      - metadata tags on compute engines
### interconnect with networks external to GCP
  - VPN: secure multi-Gbps connection over VPN tunnels
    - use cloud router to make it dynamic
  - direct peering: private connection between you and google for hybrid cloud workloads
  - carrier peering: connection through larget partner network of service providers
  - dediated interconnect: connect N X 10G transpart circuits for private cloud traffic to google cloud at google POPs
    - when you need a service level agreement
    - requires you to use the providers network typology
### cloud load balancing: load balance inbound traffic
  1.  http and https inbound traffic
    - global http(s): layer 7 load balanced based on load
      - route different urls to different back ends
      - put your application behind a single & global anycast IP to the entire internet
      - load balances traffic among all your backend instances
      - integrated with GCP CDN
  2. non http/https inbound traffic
    - global ssl proxy: layer 4 load balancing of no https ssl traffic based on load
      - supported on specific port numbers
    - global tcp proxy: layer 4 load balancing of non ssl tcp traffic
      - supported on specific port numbers
  3. for UDP traffic and TCP(non ssl) traffic
    - regional: load balancing of tcp (non ssl), udp on any port numbers
      - supported on any port number
  4. for internal tiers of multi-tier applications
    - regional internal: load balancing of traffic inside a vpc
      - use for the internal tiers of multi tier applications
    - accepts traffic on a GCP internal IP address and load balances it across compute engine VMs
### Cloud DNS:
  - create managed zones, then add, edit, delete DNS records
  - programmatically manage zones and records using restful APIs or CLI or console
### Cloud CDN:
  - distributed edge caches to cache content close to end users

## compute infrastructure for applications
  - cloud architectures: from managed infrastructure to dynamic infrastructure
    1. IaaS: infrastructure as a service
      - compute engine: general computing workloads
        - deploy your app in virtual machines
    2. Hybrid: incorporates IaaS and PaaS
      - kubernetes engine: container based workloads
        - deployr app in containers
    3. PaaS: platform as a service: google provides the infrastructure for your app so you can focus on your code
      - app engine: focus on code and with less responsibility for managing infrastructure/provisioning
        - flex: use any runtime you want with full control over the environment
          - web and mobile applications
          - container based workloads
        - standard: use one of the supported runtimes with finer grain scaling
          - web and mobile applications
    4. Serverless: no responsibility for managing infrastructure
      - BaaS: Backend as a service
        - database services
        - authentication services
      - FaaS: functions as a service
        - cloud functions: you supply chunks of code for business logic triggered by events
          -
### Compute Engine
  - run a VM
    - OS
    - memory
    - # of virtual CPUs
    - persistant storage
      - standard
      - ssd
      - attach a local SSD that doesnt last when the VM is terminated
  - types of VMs
    - preemptible VM: give compute engine permission to terminate it if its resources are needed elseware
    -
### kubernetes
  - Container Based virtualization is different than hypervisor (regular VM) based virtualization
    - container: app -> lib -> container runtime -> host OS + kernel -> hardware
      - give processes their own namespace
      - each container does not have
      - consistenc yacross dev, testing, prod env
      - loose coupling between app and operating system layers
      - simplified migration between on premis and cloud envs
      -
    - hypervisor: app -> lib -> guest OS -> hypervisor -> hardwar
  - kubernetes: orchestration layer for containers
    - uses the docker container
    - POD: a group of containers that can be deployed together
      - you can perform rolling updates, which incrementally replaces containers in pods with new ones without downtime
    - cluster: a group of machines where kubernetes can schedule containers
      - node: a machine
      -
  - kubernetes engine: managed service, a hybrid IaaS and PaaS (sits in the middle)
    - build manage and delete a  cluster with arbitrary requirements
    - give kubernetes a description of the application config, and kubernetes manages
  - google cloud container builder: create docker container images from app code in google cloud storage
  - google container registry: docker image storage for a specific project
### app engine
  - cost
    - standard environment: pay per instance class after daily free use with automatic shutdown
    - flexible environment: pay for resource allocation per hour, no automatic shutdown
  - manages the hardware and networking infrastructure required to run your app
  - you give app engine your code, and it handles the rest
    - nosql dbs
    - in-memory caching
    - load balancing
    - health checks
    - logging
    - user authentication
    - auto scaling based on traffic
  - characteristics
    - you pay for resources you use
    - for apps where the workload is highly variable  or unpredictable like web apps and mobile backends
  - standard environment
    - no ssh
    - instance starts up in milliseconds
    - network access only via app engine services
    - simple deployment experience
    - fine grained auto scale
    - free daily usage quota for some services
      - low utilization apps may run at no charge
      - runtime: the executable environment to run your application
        - python
        - java
        - php
        - GO
    - sdks
      - multiple SDK kits in various languages
      - simple commands for deployment
    - sandbox
      - your code must run in a sandbox
      - independent of hte hardware, operating system, or phsyical locatino of the server your app is running on
      - constraints
        - app cant write to the local file system
          - must use a db service
        - all requests have a 60 second timeout
        - you cant install arbitrary third party software
    - workflow
      1. dev and test locally
      2. use SDK to deploy to app engine
      3. app engine automatically scales and reliable serves the application
        - app engine can access a variaty of services using dedicated apis
          - nosql datastore
          - caching via memcache
          - searching
          - logging
          - task queues
          - scheduled tasks
          -
  - flexible environment
    - lets you specify the container your app engine runs in
      - no sandbox model like standard environment
      - docker containers run in compute engine machine VMs
    - build and deploy apps with a click
    - can access app engine resources
    - instances startup in minutes
    - can turn on SSH but its off by default
    - can write to local disk for scratch space
    - can make calls to network without going through app engine
    - supports any language
    - use case
      - web and mobile applications
      - container based workloads
      -
  - notes
    - app engine has a development environment
      - activate cloud shell
      - git clone git clone https://github.com/GoogleCloudPlatform/appengine-guestbook-python
      - click web preview in cloud shell port `:8080`
  - YAML: templating language used by many google cloud services
  - disabling deployed applications
    - App Engine offers no option to undeploy an application. After an application is deployed, it remains deployed, although you could instead replace the application with a simple page that says something like "not in service."
      - However, you can disable the application, which causes it to no longer be accessible to users.
      - `home -> app engine -> settings -> disable application`

## API management tools
  - have a well defined interface that abstracts away needless details
  - documented interface
  - the underlying implementation can change as long as the interface doesnt
  - when you have to change an API
    - always version your API
    - consumers should be able to specify the API version they want to use
### cloud endpoints
  - develop, deploy, protect and monitor APIs based ont he open APIs specification or GRPC
  - distributed api management through api console
  - expose the api using a restful interface
  - control access and validate calls with json web tokens and google api keys
  - identify web, mobile users with Auth0 and firebase
  - generate client libraries
  - monitor and log use
  - deploys a proxy infront of your application
  - support
    - app engine flexible environment: support android clients
    - kubernetes engine: supports ios clients
    - compute engine: supports javascript clients
    -
### apigee edge
  - design, secure, analyze and scale your APIs for legacy backends
  - platform for making APIs available to your customers and partners
  - containers analytics, monetization, and a developer portal
  - use cases
    - replaing a legacy application
      - use apigee to standup microservices that replace the legacy applications services one by one

## Storage
  - comparisons
    - cloud storage
      - binary/object store
      - large or rarely accessed unstructured data
      - read write latency: medium
      - typical size: any
      - storage type: object
      - NOT FOR: structured data, building fast apps
    - datastore:
      - scalable store for structured data
      - GAE apps,
      - structured pure-serve use cases
      - read wriet latency: medium
      - typical size: less than 200 tb
      - storage type: document
      - NOT FOR: relational or analytic data
    - Bigtable:
      - high volume, low latency database
      - flat, heavy read/write, analytic data
      - read wriet latency: low
      - typical size: 2tb-10tb
      - storage type: key value
      - NOT FOR: high structure or transactional data
    - CloudSQL
      - well-understored VM Based RDBMS
      - web frameworks
      - existing applications
      - read write latency: low
      - typical size: less than 10 tb
      - storage type: relational
      - NOT FOR: scaling, analytics, heavy writes
    - Spanner:
      - relational DB service
      - low latency, tansactional systems
      - read write latency: low
      - typical size: any
      - storage type: relational
      - NOT FOR: analytic data
    - Bigquery
      - autoscaling analytic data warehouse
      - interactive analysis of static datsets
      - read write latency: high
      - typical size: any
      - storage type: columnar
      - NOT FOR: building fast apps
  - choosing a storage option
    - based on application type
    - based on workload
  - object storage: storage of BYTES that are addressed with a unique key, e.g. URLs
    -
  - file storage: hierarchy of folders
  - block storage: OS manages data as chunks of disk
  - cost
    - cost per GB of data stored per month
    - egress & data transfer harges
    - nearline + coldline storage has access fee per GB of data read
  - uploading data
    - storage transfer service: schedule and manage batch transfers from other cloud providers, other regions, http endpoints
    - transfer appliance: hardware google sends you to load up data, and ship it back to google
      - up to a petabyte of data
    - online transfer: using GSUTIL or google console drag n drop
  - syncing with other GCP services
    - bigquery: import and export tables
    - app engine: object storage, logs, and datastore backups
    - compute engine: startup scripts, general object storage
    - cloud sql: import and export tables
### Caching
  - redis labs
  - memcached cloud
### Cloud Storage
  - unified object storage allowing you to serve, analyze and archive data/objects/blobs
  - built for availability, durability, scalability, and consistency
  - full managed scalable service
    - no need to provision capacity ahead of time
    - data encrypt at rest and in transit
  - online and offline import services
  - objects
    - has metadata but is treated as just bytes with no structure
      - the only key is the object name
    - versioning:
      - history of all changes to an object
      - can list objects, restore objects to an older state, or permanently delete versions
    - accessed via HTTP
      - includes ranged gets to retrieve portions of data
  - NOT FOR
    - file storage
    - block storage
  - petabytes of data, maximum unit size of 5 terabytes per object
  - Use cases
    - storing files
    - images, videos, objects and blobs, any unstructured data, static website hosting, backups
      - includes end-user uploaded content
    - for structured/unstructured binary and immutable large object storage
      - each object is given a URL
      - objects are organized in buckets, in geographic locations
    - immutable blobs larger than 10 megabytes e.g. images/movies
  - Permissions
    - IAM roles: project -> bucket -> object
    - ACL: access control Lists
      - scope: WHO can perform specific actions
      - permission: WHAT can they do
  - Storage classes
    - all have consistent APIs with millisecond access
    - cost: high to low
      - storage
        - multi-regional
        - regional
        - nearline
        - coldline
      - retrieval
        - coldline
        - nearline
        - regional
        - multi-regional
    - multi-regional:
      - content storage and delivery
      - most frequently accessed data
      - SLA: 99.95% availability
      - stored in broad geographical locations, e.g. US or ASIA
        - cloud storage will store your data in at least 2 regions within the geographical location
    - regional:
      - in-region analytics, transcoding
      - accessed frequently within a region, e.g. data closer to compute engine or kubernetes clusters
      - 99.90%
      - stored in a specific region
    - nearline storage:
      - long-tail content, backups
      - low cost, highly durable, for infrequently accessed data
      - for read/writes for once a month or less
    - cold line storage:
      - archiving, disaster recovery
      - low cost, highly durable, for data achiving, online backup, and disaster recovery
      - accessed at most once per year
      - 90 day minimum storage duration, cost per data access,

### Cloud Datastore
  - fully managed NoSQL horizontally scalable document store
  - designed to automatically scale to very large datasets, sharding, and replication
    - terabytes of capacity
    - maximum unit size of one megabyte per entity
    - offers transactions that affet multiple db rows
  - use cases
    - for durable key-value data
    - best choice for high value application data
      - user profiles, shopping carts, orders, etc.
    - store semi-structured or hierarchical data
    - managing multiple indexes over each entity
    - crossroad transactions
    - integration point for app engine and compute engine with cloud
    - support for transactions
    - sql like queries datastore as the integration point
  - characteristics
    -
    - SQL like queries

### Big Table
  - big data sparsely populated nosql wide column
    - petabytes of capacity
    - maximum unit size of 10 megabytes per call and 100 megabytes per row
  - same open soruce API as HBase (the native DB for hadoop)
  - can increase your machine count without any downtime
  - handles upgrades and restarts transparently
  - data is encrypted both in flight and at rest
  - built for fast key-value lookup and scanning over a defined key range
    - similar to a spreadsheet that gives you access to anyset of columns from continuous rows by searching only the value in the first column, the key
    - updates to individual rows are atomic
  - use cases
    - operational/analytical applications
      - user analytics or, financial data analysis, internet of things
      - for analytical data with heavy read/write events like adtech/financial or iot data
    - storing large amounts of single-keyed data (e.g. a hash table)
    - mapReduce operations
  - NOT FOR
    - if you need multi-row transactions

### Cloud SQL and Google Cloud Spanner
  - spanner uses real primary keys and interleaved child records instead of forein keys
    - Cloud SQL has foreign keys
  - offers mysql and postgresql dbs as a service
  - characteristics
    - transactions: a set of database changes as all or nothing, either they all get made or none get made
    - provide several replica services like read, fallover, and external replicas
    - can replicate data between zones with automatic failover
    - can scale both vertically by changing the machine type
    - can scale horizontally via read replicas
    - include network firewalls, and customer data is encrypted when on googles internal networks
    - supports sql workbench, toad, etc.
#### Cloud SQL
  - managed service providing replication, failover, backups
    - can replicate a master instance to one/more read-replicas
    - failover to make your data highly available
    - enable automated backup that contains data you need to protect from loss/damage
  - terabytes of capacity
  - cloud SQL Proxy
    - proxy allows for secure access to your cloud SQL second gen instances without whitelisting or configure SSL
      - uses cloud sql API to communicate with GCP
        - must provide a valid user account
    - create a proxy (client) that runs in your local environment
    - your app communicates with the proxy using a standard db protocol used by your database
    - the proxy uses a secure tunnel to communicate with its companion process running on the cloud server
  - use cases
    - best for web frameworks and existing applications
    - storing user creds and customer orders
    - structured data
    - OLTP (online transaction processing) workloads
    - applications using mysql/pgs
#### Cloud Spanner
  - fully mannaged relational db service
    - strong consistency
    - horizontal scalability
    - automatic synchronous replication for high avialiabilty
    - multi-region replication
    - transactional consistency at a global scale, schemas, SQL,
  - petabytes of dapacity
    - divides data among servers by key ranges
  - considerations
    - avoid monotonically increasing/decreasing keys
      - instead hash the key and spread the rights among n-shards
    - make sure writes are well distributed and load the data using multiple workers
    - use interleaved tables to establish hierarchy
    - don't create non-interleaved indexes on columns with monotonically increasing or decreasing keys
      - this causes all your inserts to be directed to a single instance
      - always created indexes after you bulk upload your data
  - use cases
    - mission critical OLTP (online transaction processing) applications
    - if you have outgrown any relational dbs
    - are sharding your databases for throughput high performance
    - need transactional consistency
    - for large scale applications that are larger than two terabytes
    - full sql support for  system
    - whenever high I/O global consistency is required

## Big Data and Machine Learning
  - requires investments in specific infrastructure and data processing
  - building and maintaining compute heavy data and analytics systems
  - real time analytics
  - hot keys: situations where proportionately large chunks of your input get mapped to the same cluster in a distributed system
    - e.g. in map/reduce transformations

### Big Data
  - integrated serverless platform
### Cloud dataproc
  - fast way to run data mining and analysis in datasets of known size
  - you have to request a Hadoop cluster
    - built in 90 seconds
    - uses compute engine virtual machines (you specify the type and number of VMs)
    - can scale up and down
    - can customize the default configuration
    - monitor using stackdriver
  - cost
    - pay for what you use per hour for the lifetime of the cluster
    - all cloud dataproc clusters are built in one second clock time increments: and you pay for the time it takes to build (1 minute minimum)
      - save money on the cost of the cluster by configuring the build process to use preemptible compute engine instances for your batch processing
        - requires that your jobs can be restarted cleanly if they're terminated
        - around 80% cheaper
  - managed services
    - apache hadoop: open source framework for big data based on the mapreduce programming model
    - mapreduce: one function 'the map' runs in parallel with a massive dataset to produce intermediate results, another function the 'reduce' builds a final result set based on all of the intermediate results
    - spark & spark sql:
      - do data mining
      - MLliB: machine learning libraries to run classification algorithms to discover patterns through machine learning
    - pig,
    - hive
  - other use cases (extension of use cases for the managed services above)
    - when you have a dataset of known size
      - NOT when your data shows up in real time
    - when you want to manage your dataset yourself
### cloud dataflow
  - unified programming model and managed service to build data pipelines for batch and streaming/continous data
    - transform-based programming model
  - develop and execute various data processing patterns
  - ETL (extract, transform, and load)
  - batch computation
  - continuous computation
  - full automates the management of whatever processing resources are required
    - no need to spin up a cluster or size instances
    - takes responsibility for operational tasks like resource management and performance optimization
  - use cases
    - when you have real time data
    - your data has an unpredictable size or rate
  - example
    - each step below is elastically scaled, i.e. the service provides all resources on demand
      - has automated and optimized worked partitioning built in which can dynamically rebalance lagging work
      - no need to manage/scale
    1. dataflow pipeline reads data from a source (e.g. a BigQuery table)
    2. transforms/processes the data in a variety of ways
      - map operations
      - reduce operations
    3. writes its output to a sink (e.g. cloud storage)
  - use cases
    - ETL: extract/transform/load pipelines to move, filter, enrich and shape data
    - data analysis: batch or continuous computation using streaming
      - fraud detection
      - iot analytics
      - health care
      - logistics
      - click stream
      - point of sale
      - segmentation analysis
    - orchestration: create pipelines that coordinate internal/external services
    - real time applications
      - personalizing user expeeriences
### BigQuery
  - fuly managed data warehouse for analytics
  - can scan terabytes in seconds and petabytes in minutes
  - provides near real-time interactive (adhoc) analysis (SQL 2011) of massive datasets (hundreds of TBs)
  - stream data at 100k rows per second
  - no cluster maintenance
  - SLA: 99.9% availibility
  - Data stored in is highly durable. Google stores your data in a replicated manner by default and at no additional charge for replicas.
  - data can be kept in any region
    - compute and storage are separated with a terabit network in between
  - getting data into bigquery
    - stream it at 100k rows per second
    - cloud storage
    - cloud datastore
  - datasets can be shared with people in different projects
  - cost
    - free monthly quotas
    - separate costs for storage and computation (queries)
      - storage:
        - automatic discount for long-term data storage automatically
        - sharing does NOT impact your cost or performance
          - but those users will be charged for running queries
      - queries: incur charges based on the amount of data they process:
        - when you submit a query, you pay for the compute nodes only for the duration of that query.
        - don't have to pay to keep a compute cluster up and running.
  - terms
    - Datasets: a grouping mechanism that holds zero or more tables.
      - the lowest level unit of access control
      - owned by GCP projects.
      - Each dataset can be shared with individual users.
    - Tables: a row-column structure that contains actual data.
      - Each table has a schema that describes strongly typed columns of values.
      - Each table belongs to a dataset.
  - use cases
    - big data analystics warehousing, analytics, and processing
    - OLAP (online analytic processing) workloads
    - big data exploration and processing
    - reporting via BI tools
    - read and write data via cloud dataflow, hadoop, or spark
    - run microsoft SQL
### Microsoft SQL Server
  - you can run SQL Server images on Google Compute Engine
    - can be preloaded with SQL Server
  - supported versions
    - SQL Server Standard, Web, and Enterprise
  - NOT a managed service
# Storage options for mobile
  - Cloud storage for firebase
    - overview
      - stores user generated data and files to google cloud storage
      - mobile and web access to google cloud storage
      - serverless third0party authentication and authorization
    - use cases
      - images, pictures, and videos
      - objects and  blobs
      - unstructured data
  - firebase realtime database
    - store and sync data with Firebase's NoSQL Cloud database
    - overview
      - realtime
      - NoSQL JSON database
    - use cases
      - offline responsiveness
      - mobile and web applications
      - real time
  - Fire base Hosting
    - fore static resources for web apps
    -
    - overview
      - mobile and web content hosting
      - production grade
    - use cases
      - automic release management
      - URL rewriting
      - JS App support
      - firebase instegration
      -
### cloud pub/sub
  - scalable and flexible enterprise messaging for events in realtime and stream analytics
    - on demand scalability beyond one million messages per second
  - application components make push/pull subscriptions to topics
  - supports offline consumers
  - provides at least once delivery
    - theres a small chance some messages might be delivered more than once
  - use cases
    - decoupling applications/systems: allow each to send/receive messages permitting you to then scale them independently
    - many-to-many asynchronous messaging
    - when your data arrives at high and unpredictable rates
    - analyzing streaming data (e.g. with cloud dataflow)
    - push notifications for cloud-based applications
    - connect applications across GCP (e.g. push/pull between compute and app engine)
  - cost
    -
### cloud datalab
  - managed service: interactive tool for large-scale data exploration, transformation, analysis and visualization
    - built on `jupyter notebook` which lets you create web based notebooks containing python code that can be run interactively and view the results
  - runs in a compute engine VM
  - intersperse data anlsysis with comments about the results
  - workflow
    1. specify the VM type you want and what GCP region it should run in
    2. when it launches, presents an interactive python environment thats ready to use
      - orchestrates multiple GCP services automatially
    3. visualize your data with google charts or map plot line
      - many existing packages for statistics, machine learning, and others
  - cost
    - only pay for the resources you use
    - no charge for datalab itself
  - integrations
    - BigQuery: analyze and deploy models
    - compute engine
    - cloud storage:
  - languages
    - python
    - sql
    - javascript

## Machine Learning Platform
  - Machine Learning: one branch in the field of AI
    - a way of solving problems without explicity coding the solution
    - human coders build systems that improve themselves over time through repeated exposure to sample (training) data
  - examples
    - youtube
    - photos
    - google mobile app
    - google translate
  - google provides a platform to generate your own training models or use pre-trained models built by google
    - use cases:
      - for structured data:
        - classification and regression tasks
          - customer churn analysis
          - product diagnostics
          - forecasting
        - recommendation engine for content personalization and cross/up-sales
        - anomaly detection
          - fraud detection
          - sensor diagnostics
          - log metrics
      - for unstructured data:
        - image and video analytics
          - identifying
            - damanged shipment
            - styles
          - flagging content
        - text analytics
          - call centers
          - blog analysis
          - language identification
          - topic classification
          - sentiment analysis
#### TensorFlow
  - open source tool to build and run neural network models
  - platform support:
    - CPU:
    - GPU:
    - mobile:
    - server:
    - cloud:
  - Tensor processing units: hardware devices designed to accelerate machine learning workloads with TensorFlow
    - available with compute engine VMs
      - each cloud TPU provides up to 180 teraflops of performance
  - cost:
    - pay only for what you use
#### Cloud ML
  - fully managed machine learning service
    - works on any type of data of any size
    - can take any tensorflow model and perform large-scale training on a managed cluster
  - familiar notebook-based developer experience
  - optimized for google infrastructure
  - Integrations
    - BigQuery
    - cloud storage

#### Machine Learning APIs
  - pre-trained machine learning models built by google made available through APIs
  - speech api: stream results in real time, detects 80 languages and variants
    - accessible from any device
    - highly accurate even in noisy environments
    - use cases
      - convert audio to text in real time
      - enable command and control through voice
  - vision API: analyze and identify objects, landmarks, text, and content with a simple API
    - quickly classifies images into thousands of categories
    - detects individual objects within images
    - finds and reads printed words contained within images
    - detect inapropriate content
    - image sentiment analysis
    - extract text
  - translate api: language translation including detection
    - translate arbitrary strings between thousands of language pairs
    - programtically detect a documents language
  - natural language api: offers a variety of natural language understanding technologies
    - supported languages:
      - english
      - spanish
      - japanese
    - use cases
      - syntax analysis: breaking down sentences into tokens: identifying the noun, verbs and other parts of speach to figure out the relationship between words and reveal the structure and meaning of text
      - entity recognition: parse text and flag mentions of people, organizations, etc, to extract information about items mentioned in text documents, new articles and blog posts
  - video intelligence API:
    - annotate videos in a variety of formats
    - use cases:
      - detect scene changes
      - flag inapropriate content
      - identify key entities (nouns) within your video and when they occur
        - make video content searchable and discoverable



# OLD: LinkedIn (Lynda) Learning
# basics
  - GCP: google cloud Platform
  - GCP Resources:
    - physical assets: computers, hard disk drives
    - virtual resources: VMs
    - Google data centers:
      - located in a global region: Central US, w. Europe, E. Asia
      - each reach has multiple zones  which are isolated from each other
        - asia-east1-a
    - global resources:  can be accessed by any other resource, across regions and zones. These global resources include
      - preconfigured disk images,
      - disk snapshots, and
      - networks
    - regional resources: static external IP addresses.
      - , you wouldn't want to attach a disk in one region to a computer in a different region because the latency you'd introduce would make for very poor performance. Thankfully, GCP won't let you do that; disks can only be attached to computers in the same zone.
    - zonal resources: VM instances, their types and disks
  - GCP Projects: Any GCP resources that you allocate and use must belong to a project. You can think of a project as the organizing entity for what you're building
    - project is made up of the settings, permissions, and other metadata that describe your applications
      - A project name, which you provide.
      - A project ID, which you can provide or GCP can provide for you.
      - A project number, which GCP provides.
    - The resources that each project contains remain separate across project boundaries; you can only interconnect them through an external network connection.
  - Services
    -
# services
  - GCP gives you three basic ways to interact with the services and resources.
      - GUI
    - GCP console
    - CLI
      - Google cloud SDK provides gcloud cl tool
      - cloud shell: browser-based interactive shell environment
    - client libraries
      -
## Compute: virtual machines
  - Compute Engine: Virtual Machines
  - App Engine: PaaS for apps and backends
  - Kubernetes engine: containers
  - cloud functions: event driven serverless compute platform
  - Containers & Container Management
  - Functions and Lambdas (serverless)
  -
## storage: files and databases
  - Storing
    - cloud storage for firebase hot files: frequently accessed
    - cloud filestore: cold files: archival
    - Persistent Disk: block storage for VMs: (also a type of hot file)
  - Data Services
    - NoSQL: highly available and eventually consistent
      - cloud bigtable: wide-column db service
      - cloud datastore: nosql document db service
    - RDBMS:
      - Cloud SQL: mysql + postgres
      - cloud spanner:
    - Hadoop & Spark
## Big Data
  - data pipelines: ability to string together different data services as you process data across different workloads
  - data warehouses: very large data storage for read only / infrequently updated enterprise reporting
  - data science notebooks:
    - jupiter notebooks, interactive webpages that allow computation & analysis & visualizations, pairs very well with ML
## other services: networking, ML, etc.
### Identity & Security
  - IM: Identity & Access Permissions
### Management & Monitoring
  - stack driver
### Developer Tools
  - Gcloud: scripting tool
  - IDE Integrations:
    - java
    - visual studio (.net)
## Machine Learning
# architecture
  - what are the business requirements?
    - buusiness use cases and product strategy
    - cost optimization
    - supporting the application design
    - integration
    - movement of data
    - tradeoffs
    - build, buy or modify
    - success measurements (e.g., Key Performance Indicators (KPI), Return on Investment (ROI), metrics)
  - Designing a solution infrastructure that meets technical requirements. Considerations include:
    - high availability and failover design
    - elasticity of cloud resources
    - scalability to meet growth requirements
  - Designing network, storage, and compute resources. Considerations include:
    - integration with on premises/multi-cloud environments
    - identification of data storage needs and mapping to storage systems
    - data flow diagrams
    - storage system structure (e.g., Object, File, RDBMS, NoSQL, New SQL)
    - mapping compute needs to platform products
  - 1.4 Creating a migration plan (i.e., documents and architectural diagrams). Considerations include:
	 - integrating solution with existing systems
	 - migrating systems and data to support the solution
	 - licensing mapping
	 - network and management planning
	 - testing and proof-of-concept
 - 1.5 Envisioning future solution improvements. Considerations include:
	 - cloud and technology improvements
	 - business needs evolution
	 - evangelism and advocacy
 - Section 2: Managing and provisioning solution Infrastructure
	 - 2.1 Configuring network topologies. Considerations include:
  	 - extending to on-premises (hybrid networking)
  	 - extending to a multi-cloud environment
  	 - security
  	 - data protection
	 - 2.2 Configuring individual storage systems. Considerations include:
	 -
  	 - data storage allocation
  	 - data processing/compute provisioning
  	 - security and access management
  	 - network configuration for data transfer and latency
  	 - data retention and data lifecycle management
  	 - data growth management
	 - 2.3	Configuring compute systems. Considerations include:
	 -
  	 - compute system provisioning
  	 - compute volatility configuration (preemptible vs. standard)
  	 - network configuration for compute nodes
  	 - orchestration technology configuration (e.g. Chef/Puppet/Kubernetes)
  	 - Section 3: Designing for security and compliance
	 -
	 - 3.1	Designing for security. Considerations include:
	 -
  	 - Identity and Access Management (IAM)
  	 - data security
  	 - penetration testing
  	 - Separation of Duties (SoD)
  	 - security controls
	 - 3.2 Designing for legal compliance. Considerations include:
	 -
  	 - legislation (e.g., Health Insurance Portability and Accountability Act (HIPAA), Children’s Online Privacy Protection Act (COPPA), etc.)
  	 - audits
  	 - certification (e.g., Information Technology Infrastructure Library (ITIL) framework)
 - Section 4: Analyzing and optimizing technical and business processes
	 -
	 - 4.1 Analyzing and defining technical processes. Considerations include:
	 -
  	 - Software Development Lifecycle Plan (SDLC)
  	 - continuous integration / continuous deployment
  	 - troubleshooting / post mortem analysis culture
  	 - testing and validation
  	 - IT enterprise process (e.g. ITIL)
  	 - business continuity and disaster recovery
	 - 4.2 Analyzing and defining business processes. Considerations include:
	 -
  	 - stakeholder management (e.g. Influencing and facilitation)
  	 - change management
  	 - decision making process
  	 - customer success management
	 - 4.3 Developing procedures to test resilience of solution in production (e.g., DiRT and Chaos Monkey)
	 -
 - Section 5: Managing implementation
	 -
	 - 5.1 Advising development/operation team(s) to ensure successful deployment of the solution. Considerations include:
	 -
  	 - application development
  	 - API best practices
  	 - testing frameworks (load/unit/integration)
  	 - data and system migration tooling
	 - Section 6: Ensuring solution and operations reliability
	 -
  	 - 6.1 Monitoring/Logging/Alerting solution
  	 -
  	 - 6.2 Deployment and release management
  	 -
  	 - 6.3	Supporting operational troubleshooting
  	 -
  	 - 6.4	Evaluating quality control measures