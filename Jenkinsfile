pipeline {
    agent any
    stages {
        stage ('Build') {
            steps {
                echo 'Hello MAHER'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("vigneshsweekaran/hello-world:maher")
                }
            }
        }
	    stage('Pushing Docker Image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_credential') {
                        docker.image("vigneshsweekaran/hello-world:maher").push()
                        docker.image("vigneshsweekaran/hello-world:maher").push("latest")
                    }
                }
            }
        }
        stage('Deploy'){
            steps {
                sh "docker stop hello-world | true"
                sh "docker rm hello-world | true"
                sh "docker run --name hello-world -d -p 9004:8080 vigneshsweekaran/hello-world:maher"
            }
        }
    }
}
