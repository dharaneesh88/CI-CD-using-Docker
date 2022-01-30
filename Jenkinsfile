pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/dharaneesh88/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:$BUILD_NUMBER .' 
                sh 'docker tag samplewebapp:$BUILD_NUMBER dharaneeshd/pipeline:$BUILD_NUMBER'
                
               
          }
        }
     
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 dharaneeshd/pipeline:$BUILD_NUMBER"
				
 
            }
        }
 
stage('push docker image to docker hub') {
             
            steps 
			{
                sh "docker login -u dharaneeshd -p Devops@1234"
		sh "docker push dharaneeshd/pipeline:$BUILD_NUMBER"
				
 
            }
        }
	 
	 
    }
	}
    
