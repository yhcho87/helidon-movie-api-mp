def repository = 'movie'
def appName = 'helidon-movie-api-mp'
def tenancy='apackrsct01'
def ocir='icn.ocir.io'
def imageTag = "${ocir}/${tenancy}/${repository}/${appName}:latest"

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
                        sh """
                        docker login -u ${params.REGISTRY_USERNAME} -p '${params.REGISTRY_TOKEN}' ${params.DOCKER_REGISTRY}
                        docker build -t ${imageTag} .
                        docker push ${imageTag} 
                        """
		}
	}	
        stage('Deploy To Kubernetes'){
		
			steps {		
                                sh """
                                  kubectl create ns movie
                                  kubectl create secret docker-registry ocirsecret --docker-username='apackrsct01/oracleidentitycloudservice/donghu.kim@oracle.com' --docker-password='Kyz3ux<K68O})_mAW[HH'  --docker-server=icn.ocir.io --docker-email='donghu.kim@oracle.com' -n movie 

                                """
}
}
}
}
