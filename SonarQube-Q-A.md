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

3. Maven or Gradle Installed (if using Java projects Also if others select as per that like npm - nodejs)

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



