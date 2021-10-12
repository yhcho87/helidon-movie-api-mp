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
        /*
        *stage('Build Image and push') { 
        *       steps {		
        *                sh """
        *                docker login -u ${params.REGISTRY_USERNAME} -p '${params.REGISTRY_TOKEN}' ${params.DOCKER_REGISTRY}
        *                docker build -t ${imageTag} .
        *                docker push ${imageTag} 
        *                """
	*	}
	*}	
        */
        stage
        stage('Deploy To Kubernetes'){
          steps{
            script {
              kubernetesDeploy(configs: "kube-helidon-movie-api-mp-config-direct.yml", kubeconfigId: "kubeconfig-oke")
            }
          }
        }
    }
}
