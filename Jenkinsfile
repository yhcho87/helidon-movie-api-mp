pipeline {
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git url:'https://github.com/MangDan/helidon-movie-api-mp', branch:'main'
      }
    }

    stage('Build Image and push'){			
			steps {		
				container('docker') {		
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
}
