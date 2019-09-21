node{
    stage("Git CheckOut"){
        git url: 'https://github.com/santhoshadari/spring-boot-mongo-docker.git',branch: 'master'
    }
	stage(" Maven Clean Package"){
      def mavenHome =  '/usr/share/maven'
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
    }
	stage("Build Dokcer Image") {
         sh "docker build -t santhoshadari/spring-boot-mongo:1.0.0 ."
    }
 }	
/*
pipeline{
    agent any
	environment {
	       imagetag = "santhoshadari/my-app:2.1.0"
	        }
	stages{
	  stage('SCM checkout'){
	    steps {
           git 'https://github.com/santhoshadari/my-app.git'
           }            
		 }
	  stage('MVN Clean-validate-compile'){
	     steps {
            sh label: '', script: 'mvn clean validate compile test' 	 
          }             
		 }
      stage('MVN Package'){
	     steps {
            sh label: '', script: 'mvn package' 	 
          }
		 }
	  stage('stop&remove container'){
	      steps {
		    sh """
			   docker ps -a \
			    | awk '{ print \$1,\$2 }' \
				| grep santhoshadari/my-app:2.1.0 \
				| awk '{ print \$1 }' \
				| xargs -I {} docker rm -f {}
			  """
			 //sh label: '', script: 'docker ps -a | awk \'{ print \\$1,\\$2 }\' | grep ${imagetag} | awk \'{ print \\$1 }\' | xargs -I {} docker rm -f {}'
			//sh label: '', script: "docker ps -a | awk \"{ print $1,$2 }\" | grep ${imagetag} | awk \"{ print $1 }\" | xargs -I {} docker rm -f {}"
		   }
		 }
      stage('wait_for stop container'){
           steps {
		    sh label: '', script: 'echo \'Waiting 1 minutes for deployment to complete prior starting smoke testing\''
		    sh label: '', script: 'sleep 20'
		   }
		 }		 
      stage('Build Docker image'){
	      steps {
		    sh label: '', script: "docker build -t ${imagetag} ."
		  }
		 }	  
	  stage('PUSH Docker image'){
          steps {
		   withCredentials([string(credentialsId: 'docker-pwd', variable: 'DockerHubloginpwd')]) {
           sh label: '', script: "docker login -u santhoshadari -p ${DockerHubloginpwd}" }
           sh label: '', script: "docker push ${imagetag}"
		   }
		 }	  
	  stage('remove <none> images'){
	      steps {
		    sh label: '', script: 'docker images | grep "<none>" | awk \'{ print \$3 }\' | xargs docker rmi -f'
		    }
		 }
	   stage('Deploye docker image'){
	      steps {
		    sh label: '', script: "docker run -p 9090:8080 --name myapp2 -d ${imagetag}"
		   }
		 }
	}
} */