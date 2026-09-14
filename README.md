# Jenkins 

Jenkins is still useful for **interviews and enterprise environments**.

Jenkins is one of the most popular **CI/CD automation tools** used in DevOps. It automates tasks such as **building code, running tests, creating Docker images, and deploying applications**.

For a fresher, you do **not** need to learn deep Jenkins administration initially. Focus on understanding how Jenkins works and how to create and run pipelines.

---

# 1. What is Jenkins?

**Jenkins is an open-source automation server used mainly for CI/CD.**

It can automatically perform tasks whenever developers push code.

## Simple Example

Without Jenkins:

```text
Developer
   ↓
Push code to GitHub
   ↓
Manually download code
   ↓
Build
   ↓
Run tests
   ↓
Create Docker image
   ↓
Deploy
```

With Jenkins:

```text
Developer
   ↓
Push code to GitHub
   ↓
Jenkins
   ↓
Build
   ↓
Test
   ↓
Docker Build
   ↓
Push Image
   ↓
Deploy
```

So Jenkins **automates repetitive software delivery tasks**.

### Remember:

> **Jenkins = Automation Server for CI/CD**

---

# 2. Jenkins Architecture ⭐⭐⭐⭐

Jenkins architecture describes how Jenkins receives work and executes it.

A simple architecture is:

```text
                Developer
                    ↓
                  GitHub
                    ↓
                Webhook
                    ↓
             Jenkins Controller
                    ↓
             Assigns the job
                    ↓
              Jenkins Agent
                    ↓
          Build → Test → Deploy
```

The main components are:

```text
Jenkins
│
├── Controller
│
├── Agents
│
├── Jobs
│
├── Plugins
│
├── Credentials
│
└── Pipelines
```

---

# 3. Controller / Agent Concept ⭐⭐⭐⭐⭐

This is one of the most important Jenkins concepts.

## Jenkins Controller

The **Controller** is the main Jenkins server.

It is responsible for:

* Managing Jenkins
* Managing jobs
* Scheduling builds
* Storing configuration
* Managing plugins
* Managing credentials
* Assigning work to agents

Think of the Controller as the **manager**.

```text
Controller
     ↓
"Run this build"
     ↓
Agent
```

---

## Jenkins Agent

An **Agent** is a machine that actually executes the build tasks.

For example:

```text
Controller
     ↓
Agent
     ↓
Git checkout
     ↓
Build
     ↓
Test
     ↓
Docker build
```

An agent can be:

* Linux machine
* Windows machine
* macOS machine
* Docker container
* Cloud VM

### Simple Analogy

Think about a company:

```text
Manager = Jenkins Controller

Employee = Jenkins Agent
```

The manager gives work to the employee.

### Remember:

> **Controller manages the work. Agent executes the work.**

---

# 4. Jobs ⭐⭐⭐⭐

A **Job** is a task configured in Jenkins.

For example:

```text
Build Python Application
```

A job might perform:

```text
1. Download code
2. Install dependencies
3. Run tests
4. Build application
```

Another job might:

```text
1. Build Docker image
2. Push image to Docker Hub
3. Deploy application
```

### Example

```text
Jenkins Job: Python-CI

GitHub
  ↓
Checkout code
  ↓
Install dependencies
  ↓
Run tests
  ↓
Build
```

### Remember:

> **Job = Work that Jenkins needs to perform**

---

# 5. Freestyle Project ⭐⭐⭐

A **Freestyle Project** is a simple Jenkins job where you configure the build process using the Jenkins web interface.

You don't need to write a Jenkinsfile.

For example:

```text
New Item
   ↓
Freestyle Project
   ↓
Build Steps
   ↓
Execute Shell
   ↓
python app.py
```

You can configure:

* Source Code Management
* Build triggers
* Build steps
* Post-build actions

### Example

You could tell Jenkins:

```bash
echo "Starting build"

python3 --version

echo "Running application build"

echo "Build completed"
```

Jenkins executes these commands on the agent.

---

# 6. Freestyle vs Pipeline

| Freestyle                    | Pipeline                         |
| ---------------------------- | -------------------------------- |
| Configured mainly through UI | Defined as code                  |
| Easy for beginners           | More powerful                    |
| Less flexible                | Highly flexible                  |
| Difficult to version         | Jenkinsfile can be stored in Git |
| Good for simple jobs         | Good for CI/CD                   |

For modern DevOps, **Pipeline + Jenkinsfile is more important**.

---

# 7. Pipeline ⭐⭐⭐⭐⭐

A **Pipeline** defines the complete CI/CD process.

For example:

```text
Checkout
   ↓
Build
   ↓
Test
   ↓
Docker Build
   ↓
Push
   ↓
Deploy
```

A Jenkins Pipeline allows you to define these stages and automate them.

Instead of manually performing each task, Jenkins executes the pipeline automatically.

### Example

```text
Developer
    ↓
GitHub
    ↓
Jenkins
    ↓
Checkout
    ↓
Build
    ↓
Test
    ↓
Docker Build
    ↓
Docker Push
    ↓
Deploy
```

### Remember:

> **Pipeline = Complete automated CI/CD process**

---

# 8. Jenkinsfile ⭐⭐⭐⭐⭐

A **Jenkinsfile** is a text file that contains the definition of a Jenkins Pipeline.

It is usually stored inside the Git repository.

Example:

```text
my-project/
│
├── app.py
├── requirements.txt
├── Dockerfile
└── Jenkinsfile
```

The Jenkinsfile tells Jenkins:

* What to do
* In which order to do it
* What stages to execute
* What commands to run

---

# 9. Basic Jenkinsfile Example

A simple Jenkinsfile looks like this:

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }
    }
}
```

The pipeline contains three stages:

```text
Build
  ↓
Test
  ↓
Deploy
```

---

# 10. Understanding Jenkinsfile

Let's understand the important parts.

## `pipeline`

```groovy
pipeline {
```

Defines a Jenkins Declarative Pipeline.

---

## `agent`

```groovy
agent any
```

This tells Jenkins that the pipeline can run on any available agent.

```text
Controller
     ↓
Available Agent
     ↓
Pipeline executes
```

---

## `stages`

```groovy
stages {
```

Defines the collection of stages in the pipeline.

---

## `stage`

Example:

```groovy
stage('Build') {
```

A stage represents a major phase of the CI/CD process.

Examples:

```text
Build
Test
Docker Build
Push
Deploy
```

---

## `steps`

```groovy
steps {
```

Contains the commands that Jenkins should execute for that stage.

Example:

```groovy
steps {
    echo 'Building application'
}
```

---

# 11. Pipeline Stages ⭐⭐⭐⭐⭐

Pipeline stages divide the CI/CD process into logical sections.

A real-world pipeline might look like:

```text
Pipeline
│
├── Checkout
│
├── Build
│
├── Test
│
├── Docker Build
│
├── Docker Push
│
└── Deploy
```

### Stage 1: Checkout

Get source code from GitHub.

```text
GitHub
  ↓
Jenkins
```

### Stage 2: Build

Build the application.

For example:

```bash
mvn package
```

or:

```bash
npm install
```

or:

```bash
python setup.py build
```

### Stage 3: Test

Run automated tests.

Example:

```bash
pytest
```

### Stage 4: Docker Build

Create a Docker image.

```bash
docker build -t my-app .
```

### Stage 5: Docker Push

Push the image to a container registry.

```text
Jenkins
   ↓
Docker Image
   ↓
Docker Registry
```

Examples of registries:

* Docker Hub
* Amazon ECR
* GitHub Container Registry

### Stage 6: Deploy

Deploy the application to an environment.

For example:

```text
Jenkins
   ↓
AWS
   ↓
Application
```

---

# 12. Plugins ⭐⭐⭐⭐

**Plugins extend Jenkins functionality.**

Jenkins by itself provides the core automation system, while plugins allow Jenkins to work with many different tools and technologies.

Examples:

```text
Jenkins
   │
   ├── Git Plugin
   ├── Docker Plugin
   ├── Pipeline Plugin
   ├── GitHub Plugin
   └── AWS-related plugins
```

Plugins can help Jenkins integrate with:

* Git
* GitHub
* Docker
* Kubernetes
* AWS
* Maven
* Gradle
* Slack
* SonarQube

### Example

Suppose Jenkins needs to download code from GitHub.

A Git-related plugin can provide the required integration.

```text
Jenkins
   ↓
Git Plugin
   ↓
GitHub
   ↓
Source Code
```

### Remember:

> **Plugin = Adds extra functionality/integration to Jenkins**

---

# 13. Credentials ⭐⭐⭐⭐⭐

Jenkins often needs to access external systems.

For example:

```text
Jenkins → GitHub
Jenkins → Docker Hub
Jenkins → AWS
Jenkins → Kubernetes
```

These systems may require:

* Username/password
* Access tokens
* SSH keys
* AWS credentials
* API tokens

We should **never hardcode these credentials inside the Jenkinsfile**.

Instead, Jenkins provides a **Credentials Store**.

### Example

Instead of:

```groovy
username = "myusername"
password = "mypassword"
```

store the credentials securely in Jenkins.

Then the pipeline can use them.

### Simple flow

```text
Jenkins Credentials Store
          ↓
       Jenkins
          ↓
      Pipeline
          ↓
    External System
```

### Remember:

> **Credentials = Securely stored authentication information used by Jenkins**

---

# 14. Webhooks ⭐⭐⭐⭐⭐

A **webhook** allows GitHub to notify Jenkins when an event happens.

For example:

```text
Developer
    ↓
git push
    ↓
GitHub
    ↓
Webhook
    ↓
Jenkins
    ↓
Pipeline starts
```

Without a webhook, Jenkins may need to periodically check GitHub for changes.

With a webhook:

```text
GitHub immediately tells Jenkins:
"New code was pushed!"
```

Jenkins can then start the pipeline.

### Example

Developer executes:

```bash
git push origin main
```

Then:

```text
GitHub
   ↓
Webhook
   ↓
Jenkins
   ↓
Build
   ↓
Test
   ↓
Deploy
```

### Remember:

> **Webhook = Notification from one system to another when an event occurs**

---

# 15. Build Triggers ⭐⭐⭐⭐

A **build trigger** determines **when Jenkins should start a build**.

Common triggers include:

### 1. Manual Trigger

The developer manually clicks:

```text
Build Now
```

Jenkins starts the job.

---

### 2. Webhook Trigger

GitHub sends a notification.

```text
git push
   ↓
GitHub
   ↓
Webhook
   ↓
Jenkins
   ↓
Build
```

---

### 3. Poll SCM

Jenkins periodically checks the source-code repository for changes.

Example:

```text
Every 5 minutes
      ↓
Check GitHub
      ↓
New changes?
      ↓
Yes → Build
```

---

### 4. Scheduled Build

Jenkins can run a job at a specific schedule.

For example:

```text
Every night
    ↓
Run tests
```

This can use cron-style scheduling.

### Remember:

> **Build Trigger = Condition/event that starts a Jenkins build**

---

# 16. Parameters ⭐⭐⭐⭐

**Parameters allow users to provide values when starting a Jenkins job.**

For example, suppose you have multiple environments:

```text
Development
Testing
Production
```

Instead of creating three separate jobs, you can create one parameterized job.

Example parameter:

```text
ENVIRONMENT
```

Possible values:

```text
dev
test
prod
```

When starting the job:

```text
Choose Environment:

[ dev ]
[ test ]
[ prod ]
```

Jenkins then uses the selected value.

---

# 17. Example of Parameters

Suppose the Jenkins pipeline contains:

```groovy
parameters {
    choice(
        name: 'ENVIRONMENT',
        choices: ['dev', 'test', 'prod'],
        description: 'Select deployment environment'
    )
}
```

Now the user can select:

```text
ENVIRONMENT = dev
```

The pipeline can deploy to development.

Or:

```text
ENVIRONMENT = prod
```

The pipeline can deploy to production.

### Remember:

> **Parameter = Input value provided when running a Jenkins job**

---

# 18. Complete Jenkins CI/CD Pipeline

A typical Jenkins CI/CD pipeline can look like:

```text
Developer
    ↓
Git
    ↓
GitHub
    ↓
Webhook
    ↓
Jenkins Controller
    ↓
Jenkins Agent
    ↓
Checkout
    ↓
Build
    ↓
Test
    ↓
Docker Build
    ↓
Docker Image
    ↓
Docker Registry
    ↓
Deploy
    ↓
AWS
    ↓
Application
```

---

# 19. Real-World Example

Suppose you have a Python application.

Your repository contains:

```text
python-app/
│
├── app.py
├── requirements.txt
├── test_app.py
├── Dockerfile
└── Jenkinsfile
```

Developer modifies the application.

Then:

```bash
git add .
git commit -m "Updated application"
git push origin main
```

GitHub receives the code.

Then:

```text
GitHub
   ↓
Webhook
   ↓
Jenkins
   ↓
Pipeline starts
```

Jenkins executes:

```text
Stage 1 → Checkout
Stage 2 → Install Dependencies
Stage 3 → Test
Stage 4 → Docker Build
Stage 5 → Docker Push
Stage 6 → Deploy
```

---

# 20. Example Jenkinsfile for CI/CD

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t my-app:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                echo 'Push Docker image to registry'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy application'
            }
        }
    }
}
```

The flow is:

```text
Checkout
   ↓
Install Dependencies
   ↓
Test
   ↓
Docker Build
   ↓
Docker Push
   ↓
Deploy
```

---

# 21. Jenkins + GitHub

Jenkins can integrate with GitHub.

The basic flow is:

```text
Developer
    ↓
git push
    ↓
GitHub
    ↓
Webhook
    ↓
Jenkins
    ↓
Pipeline
```

Jenkins gets the latest source code from GitHub and executes the pipeline.

---

# 22. Jenkins + Docker

Jenkins can automate Docker operations.

For example:

```text
GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
Docker Image
   ↓
Docker Registry
```

Example command:

```bash
docker build -t my-app:latest .
```

Then:

```bash
docker push my-app:latest
```

The Docker image can then be deployed.

---

# 23. Jenkins + AWS

Jenkins can also automate deployments to AWS.

A common architecture is:

```text
Developer
    ↓
GitHub
    ↓
Jenkins
    ↓
Build
    ↓
Test
    ↓
Docker Build
    ↓
Amazon ECR
    ↓
ECS / EKS / EC2
    ↓
Application
```

For example:

```text
Jenkins
   ↓
Build Docker image
   ↓
Push image to Amazon ECR
   ↓
Deploy application
   ↓
AWS
```

---

# 24. Jenkins CI vs CD

## CI — Continuous Integration

CI focuses on automatically building and testing code.

```text
Developer
   ↓
GitHub
   ↓
Jenkins
   ↓
Build
   ↓
Test
```

---

## CD — Continuous Delivery / Deployment

CD focuses on delivering or deploying the validated application.

```text
Jenkins
   ↓
Docker Build
   ↓
Docker Registry
   ↓
Deploy
   ↓
AWS
```

Combined:

```text
GitHub
   ↓
Jenkins
   ↓
Build
   ↓
Test
   ↓
Docker Build
   ↓
Push
   ↓
Deploy
```

---

# 25. Jenkins Pipeline Failure

Jenkins automatically tracks whether each stage succeeds or fails.

For example:

```text
Checkout       ✅
Build          ✅
Test           ❌
Docker Build   ⏭️
Deploy         ⏭️
```

If the testing stage fails, later stages normally should not execute.

This protects the deployment environment from receiving code that has failed validation.

### Example

```text
Build
  ↓
Success
  ↓
Test
  ↓
FAILED
  ↓
Stop Pipeline
```

This is an important CI/CD concept.

---

# 26. Jenkins Job vs Pipeline vs Jenkinsfile

These terms can be confusing.

### Job

A **Job** is the task Jenkins executes.

```text
Job
 ↓
Build application
```

### Pipeline

A **Pipeline** defines the complete CI/CD process.

```text
Build
 ↓
Test
 ↓
Deploy
```

### Jenkinsfile

A **Jenkinsfile** is the file containing the Pipeline definition.

```text
Jenkinsfile
     ↓
Pipeline
     ↓
Jenkins
     ↓
Build → Test → Deploy
```

### Easy way to remember:

```text
Job = Task

Pipeline = Process

Jenkinsfile = Code that defines the process
```

---

# 27. Controller vs Agent

| Controller            | Agent                  |
| --------------------- | ---------------------- |
| Manages Jenkins       | Executes tasks         |
| Schedules jobs        | Runs builds            |
| Manages configuration | Runs commands          |
| Manages credentials   | Uses required tools    |
| Assigns work          | Performs assigned work |

### Easy memory:

```text
Controller = Manager
Agent = Worker
```

---

# 28. Jenkins Important Components

```text
                 Jenkins
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
   Controller      Jobs      Plugins
        │
        ↓
     Agents
        │
        ↓
   Build / Test
        │
        ↓
     Pipeline
        │
        ↓
     Deploy
```

---

# 29. Important Jenkins Terms

| Term          | Meaning                            |
| ------------- | ---------------------------------- |
| Jenkins       | CI/CD automation server            |
| Controller    | Manages Jenkins and assigns work   |
| Agent         | Executes jobs                      |
| Job           | Task configured in Jenkins         |
| Freestyle     | UI-based Jenkins project           |
| Pipeline      | Automated CI/CD process            |
| Jenkinsfile   | Pipeline-as-code file              |
| Plugin        | Adds functionality/integration     |
| Credentials   | Secure authentication information  |
| Webhook       | Event notification between systems |
| Build Trigger | Starts a Jenkins build             |
| Parameter     | Input provided to a job            |
| Stage         | Major phase of a pipeline          |
| Step          | Individual task inside a stage     |

---

# 30. Jenkins Pipeline Mental Model

Remember this:

```text
Developer
    ↓
GitHub
    ↓
Webhook
    ↓
Jenkins Controller
    ↓
Jenkins Agent
    ↓
Pipeline
    ↓
Checkout
    ↓
Build
    ↓
Test
    ↓
Docker Build
    ↓
Docker Push
    ↓
Deploy
    ↓
AWS
```

This is the most important Jenkins flow to understand as a fresher.

---

# 31. Jenkins Learning Order for a Fresher

You don't need to learn everything in Jenkins immediately.

Follow this order:

```text
1. What is Jenkins?
        ↓
2. Jenkins Architecture
        ↓
3. Controller
        ↓
4. Agent
        ↓
5. Jobs
        ↓
6. Freestyle Project
        ↓
7. Pipeline
        ↓
8. Jenkinsfile
        ↓
9. Stages
        ↓
10. Steps
        ↓
11. Plugins
        ↓
12. Credentials
        ↓
13. Webhooks
        ↓
14. Build Triggers
        ↓
15. Parameters
        ↓
16. Jenkins + GitHub
        ↓
17. Jenkins + Docker
        ↓
18. Jenkins + AWS
```

---

# 32. What You Don't Need to Learn Initially

As a fresher, you **do not need deep Jenkins administration initially**.

Don't focus heavily on things such as:

* Advanced Jenkins controller administration
* Complex distributed architectures
* Advanced plugin development
* Jenkins internals
* Advanced security administration
* Complex agent orchestration

First become comfortable with:

```text
Jenkins
 ↓
Jobs
 ↓
Pipeline
 ↓
Jenkinsfile
 ↓
Stages
 ↓
GitHub
 ↓
Webhooks
 ↓
Credentials
 ↓
Docker
 ↓
AWS
```

Once these concepts are clear, you can move into advanced Jenkins administration.

---

# 33. Interview Questions You Should Know

### 1. What is Jenkins?

Jenkins is an open-source automation server primarily used for CI/CD.

### 2. What is a Jenkins Job?

A Jenkins Job is a configured task that Jenkins executes.

### 3. What is a Jenkins Pipeline?

A Jenkins Pipeline defines an automated sequence of CI/CD stages such as build, test, and deployment.

### 4. What is a Jenkinsfile?

A Jenkinsfile is a file that defines a Jenkins Pipeline as code.

### 5. What is a Jenkins Agent?

An Agent is a machine where Jenkins executes build and deployment tasks.

### 6. What is a Jenkins Controller?

The Controller manages Jenkins, schedules jobs, and assigns work to agents.

### 7. What is a Freestyle Project?

A Freestyle Project is a Jenkins job configured primarily through the Jenkins UI.

### 8. What are Jenkins Plugins?

Plugins extend Jenkins functionality and provide integrations with external tools.

### 9. What are Jenkins Credentials?

Credentials are securely stored authentication details used by Jenkins to access external systems.

### 10. What is a Webhook?

A webhook allows GitHub or another system to notify Jenkins when an event occurs.

### 11. What is a Build Trigger?

A build trigger determines when Jenkins should start a job.

### 12. What are Pipeline Stages?

Stages divide a pipeline into logical phases such as Build, Test, and Deploy.

### 13. What are Jenkins Parameters?

Parameters allow users to provide input values when starting a Jenkins job.

---

# 34. Final Jenkins Mental Model

The easiest way to remember Jenkins is:

```text
                 DEVELOPER
                     │
                     ↓
                  GitHub
                     │
                     ↓
                 Webhook
                     │
                     ↓
              JENKINS CONTROLLER
                     │
                     ↓
                JENKINS AGENT
                     │
                     ↓
                  JOB
                     │
                     ↓
                PIPELINE
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
     BUILD          TEST          DEPLOY
       │             │             │
       └─────────────┼─────────────┘
                     ↓
                  DOCKER
                     ↓
              DOCKER REGISTRY
                     ↓
                    AWS
                     ↓
               APPLICATION
```

### One-line revision:

> **Jenkins automates the process of taking code from GitHub, building and testing it, packaging it, and deploying it to an environment.**

### Most important things for a fresher:

```text
Jenkins
   ↓
Controller / Agent
   ↓
Jobs
   ↓
Pipeline
   ↓
Jenkinsfile
   ↓
Stages
   ↓
Plugins
   ↓
Credentials
   ↓
Webhooks
   ↓
Build Triggers
   ↓
Parameters
   ↓
GitHub + Docker + AWS
```

---

# Quick Revision

```text
Jenkins
→ CI/CD automation server

Controller
→ Manages Jenkins

Agent
→ Executes work

Job
→ Task

Freestyle
→ UI-based job

Pipeline
→ Complete CI/CD process

Jenkinsfile
→ Pipeline as code

Stage
→ Major phase of pipeline

Step
→ Individual task

Plugin
→ Adds functionality

Credentials
→ Secure authentication details

Webhook
→ Event notification

Build Trigger
→ Starts a build

Parameter
→ User input

Docker
→ Build and package application

AWS
→ Deployment environment
```

## Final Flow

```text
Developer
   ↓
GitHub
   ↓
Webhook
   ↓
Jenkins
   ↓
Controller
   ↓
Agent
   ↓
Pipeline
   ↓
Build
   ↓
Test
   ↓
Docker Build
   ↓
Docker Registry
   ↓
Deploy
   ↓
AWS
```

**Remember:**

> **Controller manages → Agent executes → Job performs work → Pipeline defines the process → Jenkinsfile stores the pipeline → Stages organize the process → Webhook triggers it → Credentials provide secure access.**

