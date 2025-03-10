# Q. What is SonarQube?
***SonarQube*** is an open-source platform for continuous code quality inspection. It analyzes source code to detect bugs, vulnerabilities, code smells, and security issues, helping developers maintain high-quality and secure code.

## Key Features of SonarQube

- **Code Quality Analysis** – Identifies bugs, vulnerabilities, and code smells.  
- **Supports Multiple Languages** – Works with Java, Python, JavaScript, C++, Go, Kubernetes YAML, and more.  
- **Static Code Analysis** – Scans the source code without execution.  
- **Security Scanning** – Detects security flaws like SQL injection, XSS, and hardcoded credentials.  
- **Integration with CI/CD** – Works with Jenkins, GitHub Actions, GitLab, Azure DevOps, etc.  
- **Quality Gates** – Blocks builds if the code doesn’t meet quality standards.  
- **Dashboard & Reports** – Provides detailed reports on technical debt, maintainability, and test coverage.  

## SonarQube Metrics

- **Bugs** – Defects that could cause failures.  
- **Code Smells** – Poor coding practices affecting maintainability.  
- **Vulnerabilities** – Security risks in the code.  
- **Technical Debt** – Time required to fix issues.  
- **Code Coverage** – Measures how much of the code is covered by unit tests.  

## SonarQube Editions
- **Community (Free)** – Basic code analysis.
- **Developer** – Advanced features like branch analysis.
- **Enterprise** – Security scanning and compliance reports.
- **Data Center** – High availability for large enterprises.

# Q. SonarQube Integration with Jenkins
Integrating SonarQube with Jenkins allows automated code analysis in CI/CD pipelines, ensuring code quality, security, and maintainability. Below is a step-by-step guide to integrate SonarQube with Jenkins.

## Prerequisites
1. Jenkins Installed with:
- Jenkins Plugins:
  - SonarQube Scanner Plugin
  - Pipeline Plugin
 
2. SonarQube Server is Running
- Admin access to SonarQube Dashboard
- Generate a SonarQube Token

3. Maven or Gradle or NPM Installed ( Use Build tool as per code stack)

## Step 1: Install SonarQube Plugin in Jenkins
1. Go to Jenkins Dashboard → `Manage Jenkins` → `Manage Plugins`.
2. Search for SonarQube Scanner Plugin.
3. Click Install and restart Jenkins.

## Step 2: Configure SonarQube in Jenkins
**Add SonarQube Server Details**
1. Go to Jenkins Dashboard → `Manage Jenkins` → `Configure System`.
2. Find the SonarQube Servers section.
3. Click Add SonarQube.
   - Name: `SonarQube`
   - Server URL: `http://<sonarqube-server-ip>:9000`
   - Authentication Token:
     - In SonarQube UI: Go to `My Account` → `Security` → Generate Token.
     - Copy the token and add it in Jenkins under **"Server Authentication Token"**.
4. Click Save.

## Step 3: Configure SonarQube Scanner
1. Go to Jenkins Dashboard → `Manage Jenkins` → `Global Tool Configuration`.
2. Find the SonarQube Scanner section.
3. Click Add SonarQube Scanner.
   - Name: `SonarScanner`
   - Install automatically: Check the box.
4. Click Save.

## Step 4: Add SonarQube to Jenkins Pipeline
Add the following Jenkinsfile:
```groovy
pipeline {
    agent any
    tools {
        maven 'Maven3'  // Make sure Maven is installed in Jenkins
    }
    environment {
        SONARQUBE_URL = 'http://<sonarqube-server-ip>:9000'
        SONAR_TOKEN = credentials('sonar-token')  // Store token in Jenkins Credentials
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/example/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.host.url=$SONARQUBE_URL -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }
        stage('Quality Gate') {
            steps {
                script {
                    timeout(time: 1, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
                }
            }
        }
    }
}
```
- Run pipeline 

## Additional Configurations
1. Quality Gate Enforcement
   To fail the pipeline if SonarQube detects issues:
   - In SonarQube UI, go to Quality Gates.
   - Set rules like:
     - Fail if Code Coverage < 80%.
     - Fail if Bugs > 0.

## Webhook for SonarQube & Jenkins
To trigger Jenkins when SonarQube analysis is complete:

1. In SonarQube UI, go to `Administration` → `Webhooks`.
2. Click Create Webhook.
   - URL: `http://<jenkins-server>:8080/sonarqube-webhook/`
3. Click Save.
  





