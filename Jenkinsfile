pipeline { 
    environment { 
        registry = "rajat2298/nodeapp" 
        registryCredential = '7838569003' 
        dockerImage = '' 
    }
    agent any 
    stages { 
	stage('Cloning our Git') { 
            steps { 
                checkout scm 
            }
        } 
        stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
        stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                    dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
    }
}
