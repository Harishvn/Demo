node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/MithunTechnologiesDevOps/spring-boot-mongo-docker.git',branch: 'master'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Build image") {
            steps {
                script {
                    sh 'docker build -t harishvn/hello .'
					
                }
            }
        }
	stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DOKCER_HUB_PASSWORD', variable: 'DOKCER_HUB_PASSWORD')]) {
          sh "docker login -u harishvn -p ${DOKCER_HUB_PASSWORD}"
        }
        sh 'docker push harishvn/spring-boot-mongo'
     }
        }        
    stage('Deploy Application in K8S') {
            kubernetesDeploy(
                configs: 'deployment.yaml', 
				kubeconfigId: 'KUBERENETES_CLUSTER_CONFIG',
				enableConfigSubtitution: true
            )
        }
		
		  }    
		}