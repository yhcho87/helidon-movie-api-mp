def repository = 'movie'
def appName = 'helidon-movie-api-mp'
def tenancy='apackrsct01'
def ocir='icn.ocir.io'
def imageTag = "${ocir}/${tenancy}/${repository}/${appName}:latest"

pipeline {
    agent any
    stages {
        /* 
        *stage('Build') { 
        *    steps {
        *       withMaven(maven: 'mvn') {
	*    	 sh 'mvn clean'	 
        *       }
        *    }
        *}
        *stage('Build Image and push') { 
        *       steps {		
        *           sh """
        *               docker login -u ${params.REGISTRY_USERNAME} -p '${params.REGISTRY_TOKEN}' ${params.DOCKER_REGISTRY}
        *               docker build -t ${imageTag} .
        *               docker push ${imageTag} 
        *           """
	*	}
	*}
        */ 
        stage('Deploy To Kubernetes'){
          steps{
              catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh "kubectl create ns  ${params.NAMESPACE}"
              }
              catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh "kubectl create secret docker-registry ocirsecret --docker-username='${params.REGISTRY_USERNAME}' --docker-password='${params.REGISTRY_TOKEN}'  --docker-server=${params.DOCKER_REGISTRY} --docker-email='donghu.kim@oracle.com' -n ${params.NAMESPACE}"
              }

              sh "kubectl apply -f kube-helidon-movie-api-mp-config-direct.yml"
            }
        }
    }
}
