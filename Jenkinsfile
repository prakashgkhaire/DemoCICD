pipeline { 
    environment { 
        registry = "prakashgkhaire/democicd" 
        registryCredential = 'docker-hub-credentials' 
        dockerImage = '' 

    }

    agent any 

    stages { 
        stage('Cloning our Git') { 
            steps { 
                git 'https://github.com/prakashgkhaire/DemoCICD.git' 
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
                sh "docker images"
                sh "docker rmi --force $registry:$BUILD_NUMBER"
            }
        }
    }
}

node {
    stage('Execute Image'){
        def customImage = docker.build("aryashreep/DemoCICD:${env.BUILD_NUMBER}")
        customImage.inside {
           sh 'echo This is the code executing inside the container.'
        }
    }
}


