pipeline { 
    environment { 
        registry = "prakashgkhaire/democicd" 
        registryCredential = 'dockerhub'
        
    } 
        agent any 
        
        stages { 
            stage('Cloning Git') { 
                steps { 
                    git 'https://github.com/prakashgkhaire/DemoCICD.git'
                    } 
                } 
            
            stage('Building image') { 
                steps{ 
                    script { 
                        docker.build registry + ":$BUILD_NUMBER" 
                        
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
    
}
