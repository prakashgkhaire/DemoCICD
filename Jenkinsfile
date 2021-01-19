pipeline { 
    environment { 
        registry = "prakashgkhaire/democicd" 
        registryCredential = 'dockerhub'
        
    } 
        agent any 
        
        stage { 
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
        }
    
}
