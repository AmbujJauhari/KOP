# KOP
Kubernetes Onboarding Platform

# Why the need for KOP

Kubernetes ecosystem is a mixture of multiple moving parts and each of them has many options and each follow different best practices. Where it gets tricky is to establish the conventions and configurations for any organization

Some of the examples of moving parts are

1. Kubernetes cluster 
    - Namespaces
    - Services 
2. Service Mesh
    - Traffic management
    - Authentication
    - Authorization
3. Application Deployment
4. Metrics Collection
5. Autoscaling (Vertical and Horizontal)
6. IAC


The above mentioned parts can be categorized into 2 sections one at cluster level and other at application level, for e.g. a organization might want to configure the authentication at the cluster level against a common LDAP and all the application deployed use the same authentication mechanism but you might want to have authorization configured at application level based on certain role allow access to particular application. Similarly certain parts of traffic management need to configured at cluster level and certain parts at the application level.

Same goes for auto scaling you can scale pods based on cpu and memory, as a dev ops admin you might want to configure that if any pod breaches 80% cpu usage it scales horizontally or you might want to create custom auto scalers like number of requests per second.

# What does KOP do ?

KOP is basically a easy UI based tool which gives you to use it in 2 modes 

1. Devops Admin
2. Application Developer

Devops Admin basically controls the settings and configuration at a cluster level, so to spin up a new cluster based on the inputs by devops admin. KOP generates the following

1. Terraform scripts to create cluster
2. Add istio service mesh configuration
    - Ingress controller
    - mTLS config
3. Create yaml files for logging and metrics collection 
4. Provide integration with Hashicorp Vault for storing secrets
5. Create spring configuration server within cluster


basically all of the things that we want to control at cluster level

When a scrum team is ready to deploy their application to K8, application owner raises a request in KOP with settings that are to be defined at an application level. 

1. This creates deployment files
2. This creates service files
3. This creates k8 CRD yaml files which are basically istio yaml files
4. auto scaler configurations like HPA or custom via KEDA
5. Creates namespace config with access to certain team members (optional)
6. 

Initially these scripts are basically committed to a repository which will trigger an automated build. This is to make sure that same package that is built from the code committed by KOP can be moved across environments from DEV to SIT to UAT to PREPROD to PROD

# Tech stack
Frontend : Flutter
Backend : Flask / Python
