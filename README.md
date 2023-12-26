# Integrating Security Testing Into The Software Development Lifecycle
<img src="https://raw.githubusercontent.com/bayulus/devsecops-jenkins-aws/d43e6146dfefaf7f5902677e2872684f4f15d64a/images/DevSecOps-%20Project%20Dissertation.jpg" >

<h2>Introduction</h2> 

In this project, I design and implement a comprehensive DevSecOps pipeline that seamlessly integrates security practices into the software development lifecycle using AWS cloud infrastructure.
  * I design and execute a DevSecOps pipeline that smoothly incorporates Static Application Security Testing (SAST), Software Composition Analysis (SCA), and Dynamic Application Security Testing (DAST) phases. This aims to illustrate how the joint work of development, security, and operations teams can actively identify and address vulnerabilities.
  * I employed SonarCloud to conduct static application security testing (SAST), utilized Snyk for software composition analysis (SCA), and employed OWASP Zap for dynamic application security testing (DAST).
  * I used  platforms and tools such as Jenkins, AWS EKS, AWS ECR, and Terraform for this project.

<h2>Environment and Tools Used</h2>

 * **AWS** - For cloud Infrastructure
 * **Jenkins** -  For continuous integration and continuous delivery (CI/CD) processes.
 * **Terraform** - For infrastructure as code (IaC), enabling the provisioning and management of cloud resources.
 * **AWS EKS** -  Amazon Elastic Kubernetes Service, for orchestrating and managing Kubernetes clusters on AWS.
 * **AWS ECR** - Amazon Elastic Container Registry, a fully managed Docker container registry for storing, managing, and deploying Docker container images.
 * **GitHub** -  For version control and collaborative software development, allowing teams to manage code repositories and track changes efficiently.

<h2>Creating Cloud Infrastructure Using Terraform</h2>
<p>The code snippet is written in HashiCorp Configuration Language (HCL) and is used for creating infrastructure with Terraform. It includes configuration settings for an AWS EC2 instance and networking configurations like Security Groups, which control inbound and outbound traffic. The configuration files articulate the desired state of the infrastructure.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/mainft.png?raw=true" >

<h2>Running Virtual Machine Created on AWS with Jenkins, Kubernetes, Docker OWASP ZAP and Maven Installed</h2>
<p>The Terraform repository contains a shell script called installjenkinszap.sh, which automates the installation and configuration of various software packages on a virtual machine. The script installs Jenkins, OWASP ZAP, Maven, Docker, Kubernetes, and Git. By integrating the script into the Terraform configuration file, it ensures that these components are installed and configured on the EC2 instance as soon as it's provisioned. This saves time and effort and ensures consistency across environments.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/8.png" >

<h2>GitHub Repository</h2>
<p>The web application's source code is stored on  in the github repositories. Jenkins server monitors the repositories for any changes using a webhook and pulls the latest code when a new commit is made. Jenkins then uses Maven to build the code, including compiling Java, resolving dependencies, and generating executable artifacts. The project's pom.xml file also includes configurations for plugins like Snyk and OWASP's dependency-check for code analysis and security checks, which Jenkins ensures are executed during the build process. Jenkins captures information about the build as it proceeds, such as errors or warnings.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/gitrepo.png?raw=true" >

_The provided repository above includes a "Jenkinsfile" containing directives for automating the complete build, testing, and code analysis procedures for the Java web application. In the repo is also a "dockerfile" that outlines the necessary steps to build an image containing the application and its dependencies. Also, The "deployment.yaml" file located in the repository serves as a means to specify a deployment resource in Kubernetes._

<h1>Implementation<h2></h2>

<h2>SAST Implementation Using SonarCloud</h2>

<p>SonarCloud is integrated into the pipeline to analyze the source code for vulnerabilities and quality issues. It scans the codebase for known vulnerabilities and code quality issues that could impact the application's security and maintainability.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/sonarcloud.PNG?raw=true" >

 * <h3>SonarCloud Build Result</h3>
 <p>Jenkins sends code to SonarCloud for analysis after the build process. The scan results show 56 bugs, 53 vulnerabilities, 138 code smells, 38 security hotspots, and 6.6% identical lines of code. SonarCloud not only identifies issues in the code, but also provides solutions to prevent them.</p>
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/18.PNG?raw=true" >

 * <h3>SonarCloud Test Result</h3>
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/19.PNG?raw=true" >
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/20.PNG?raw=true" >

<h2>SCA Implementation Using Snyk</h2>

<p>Performing an SCA scan in our code serves the purpose of identifying and addressing potential security vulnerabilities present in the third-party libraries, frameworks, and components upon which our codes in the pom.xml file depend. The integration of Snyk into our development process enables us to identify vulnerabilities within the dependencies utilized in the code.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/21.PNG?raw=true" >

 * <h3>Snyk Build and Test result</h3>
 <p>Snyk found 35 known issues with dependencies, as well as 44 other issues and 44 vulnerable paths. It not only identifies vulnerabilities but also gives guidance on how to fix them, such as using patches, different package versions, or code changes.</p>
   <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/22.PNG?raw=true" >
   <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/23.PNG?raw=true" >

<h2>Steps to Take Before Conducting a DAST Scan</h2>
<p>To start the DAST scan, the initial step is to create a Docker image called "easy" and upload it to Docker Hub using the Docker daemon on a Jenkins machine. Then, the image is moved to an Amazon ECR repository using the provided credentials and URL by logging into an AWS account. This is done to utilize the containerized application from ECR for deployment to Kubernetes for orchestration and DAST scanning. </p>

 * <h4>Code Snippet of The Build and Push Stage in the Jenkinsfile</h4>
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/26.PNG?raw=true" >

 * <h4>Image Showing A successful Jenkins Pipeline With The App Image Built and Push to ECR</h4>
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/24.PNG?raw=true" >

 * <h4>Image of The Dockerized App Image Built to Amazon ECR Ready For Deployment to Amazon Kubernetes</h4>
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/25.PNG?raw=true" >

 * <h4>Seamless Deployment of Containerized Application on AWS Kubernetes</h4>
 <p>To implement DAST on the Java application, I need to deploy it to Kubernetes after containerizing it and pushing it to ECR. This will create a seamless runtime environment and allow us to easily scale our application by adding or removing container instances.</p>
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/29.PNG?raw=true" > 
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/28.PNG?raw=true" >
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/30.PNG?raw=true" >

 <p>The java application is deployed on Kubernetes with an external IP address or Hostname. The URL for accessing the application is abf0cfbad1db94924a4f9ddf25db684d-539840078.eu-west-2.elb.amazonaws.com. Traffic from port 80 is forwarded to port 30903 on the cluster's nodes.</p>

 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/31.PNG?raw=true" >


<h2>DAST Implementation Using OWASP ZAP</h2>
<p>The next task in the DevSecOps pipeline is to perform a DAST scan on our application to simulate real-life attack scenarios on the  application.</p>

<img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/35.PNG?raw=true" >

 * <h2> OWASP ZAP Build and Test Result </h2>
 The full scan result can be found in the zap_report.html in the repo

 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/32.PNG?raw=true">
 <img src="https://github.com/bayulus/devsecops-jenkins-aws/blob/main/images/34.PNG?raw=true" >

<h1>Conclusion</h1>
<p>In this project, I conducted security testing at various stages of the software development life cycle. I conducted SAST, SCA, and DAST to implement security measures using various tools. The DevSecOps initiative goes beyond just using tools; it's about creating a culture that prioritizes security. It's about adopting a mindset that values security in every aspect. By integrating security into the development process, we're not only writing code; we're building resilient and secure solutions that can withstand evolving threats. Emphasizing early detection of vulnerabilities, closely monitoring third-party dependencies, simulating real-world attacks, and integrating practical security practices can help organizations develop more secure applications without slowing down the development process.</p>
