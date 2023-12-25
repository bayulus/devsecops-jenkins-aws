pipeline {
  agent any
  tools { 
        jdk 'java'
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
            sh '''mvn clean verify sonar:sonar -Dsonar.projectKey=devsecopssast -Dsonar.projectName=desecopssast -Dsonar.host.url=http://localhost:9000  -Dsonar.token=sqp_ee72a41c78c64bc0cf9953deb12604103a4327b3'''
			}
        } 
  }
}
