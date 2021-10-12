def repository = 'movie'
def appName = 'helidon-movie-api-mp'
def tenancy='apackrsct01'
def ocir='icn.ocir.io'
def imageTag = "${ocir}/${tenancy}/${repository}/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"

pipeline {
    agent { label 'jenkinsslave' }
    
    stages {
        
        stage('Build') { 
            steps {
	    	sh 'mvn clean'	 
            }
        }
        stage('Build Image and push') { 
               steps {		
		    		withDockerRegistry(credentialsId: 'ocir-credentials', url: "https://${ocir}") {
					      sh """				           
				            docker build -t ${imageTag} .
				            docker push ${imageTag}
				            """
					}	
				
		}	
        }
    }
}

