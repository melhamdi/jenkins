pipeline { 

  environment { 
      registry = "melhamdi/rep01" 
      registryCredential = 'dockerhub_id' 
      dockerImage = '' 
  }

  agent any 
  stages { 
      stage('Cloning our Git') { 
          steps { 
              git 'https://github.com/melhamdi/jenkins.git' 
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
                 // docker.withRegistry( '', registryCredential )
		      withDockerRegistry([ credentialsId: "registryCredential", url: "https://registry.hub.docker.com" ]){ 
                      dockerImage.push() 
                  }
              } 
          }
      } 

//      stage('Cleaning up') { 
//          steps { 
//              sh "docker rmi $registry:$BUILD_NUMBER" 
//          }
//      } 
  }
}
