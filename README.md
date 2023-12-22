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
<p>In the Terraform repo was a shell script called installjenkinszap.sh. The shell script is a sequence of commands written in a scripting language that automates the installation and configuration of various software packages and tools on the virtual machine. The shell scripts is to install Jenkins, OWASP ZAP (a security tool), Maven (a build tool), Docker, Kubernetes, and Git. By including the shell script execution in the Terraform configuration main.tf file, It ensures that these software’s components are installed and configured on the EC2 instance as soon as it’s provisioned. This seamless integration automates the setup process, saving time and effort and ensuring consistency across environments.</p>




