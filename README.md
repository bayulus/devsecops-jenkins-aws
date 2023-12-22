# Integrating Security Testing Into The Sofware Development Lifecycle
<img src="https://raw.githubusercontent.com/bayulus/devsecops-jenkins-aws/d43e6146dfefaf7f5902677e2872684f4f15d64a/images/DevSecOps-%20Project%20Dissertation.jpg" >

<h2>Introduction</h2> 

In this project, I design and implement a comprehensive DevSecOps pipeline that seamlessly integrates security practices into the software development lifecycle using AWS cloud infrastructure.
  * I design and execute a DevSecOps pipeline that smoothly incorporates Static Application Security Testing (SAST), Software Composition Analysis (SCA), and Dynamic Application Security Testing (DAST) phases. This aims to illustrate how the joint work of development, security, and operations teams can actively identify and address vulnerabilities.
  * I employed SonarCloud to conduct static application security testing (SAST), utilized Snyk for software composition analysis (SCA), and employed OWASP Zap for dynamic application security testing (DAST).
  * I used  platforms and tools such as Jenkins, AWS EKS, AWS ECR, and Terraform for this project.

<h2>Environment and Tools Used</h2>

 * AWS - For cloud Infrastructure
 * Jenkins -
 * Terraform -
 * AWS EKS -
 * AWS ECR -
 * Github - 

<h2>Creating Cloud Infrastructure Using Terraform</h2>
<p>The code snippet is written in HashiCorp Configuration Language (HCL) and is used for creating infrastructure with Terraform. It includes configuration settings for an AWS EC2 instance and networking configurations like Security Groups, which control inbound and outbound traffic. The configuration files articulate the desired state of the infrastructure.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/mainft.png?raw=true" >

<h2>Running Virtual Machine Created on AWS with Jenkins, Kubernetes, Docker OWASP ZAP and Maven Installed</h2>
<p>The Terraform repository contains a shell script called installjenkinszap.sh, which automates the installation and configuration of various software packages on a virtual machine. The script installs Jenkins, OWASP ZAP, Maven, Docker, Kubernetes, and Git. By integrating the script into the Terraform configuration file, it ensures that these components are installed and configured on the EC2 instance as soon as it's provisioned. This saves time and effort and ensures consistency across environments.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/8.png" >

<h2>GitHub Repository</h2>
<p>The web application's source code is stored on GitLab in repositories. Jenkins server monitors the repositories for any changes using a webhook, and pulls the latest code when a new commit is made. Jenkins then uses Maven to build the code, including compiling Java, resolving dependencies, and generating executable artifacts. The project's pom.xml file also includes configurations for plugins like Snyk and OWASP's dependency-check for code analysis and security checks, which Jenkins ensures are executed during the build process. Jenkins captures information about the build as it proceeds, such as errors or warnings.</p>






