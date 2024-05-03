pipeline {

        tools {
            maven 'mymaven'
        }

        agent any

        stages {
            stage('Checkout') {
                steps {
                    // Checkout the code from the repository
                    git branch: 'main', url: ' https://github.com/reshma-stani/project_xy.git '
                }
            }

            stage('Compile') {
                steps {
                    // Compile the Maven project
                    sh 'mvn compile'
                }
            }
            stage('Test') {
                steps {
                    // Run Maven tests
                    sh 'mvn test'
                }
            }
            stage('Package') {
                steps {
                    // Clean and package the Maven project
                    sh 'mvn clean package'
                }
            }
        stage('Build Image') {
                steps {

                    // Copy the WAR file to the webapps directory in the container
                    sh "docker build -t ${DOCKER_IMAGE}:latest ."
                }
            }
            stage('Push DockerImage') {
                steps {
                    withDockerRegistry(credentialsId: 'f80a6223-95e8-4a88-a9af-362d5c4a129c', url: DOCKER_REGISTRY) {
                        sh "docker push ${DOCKER_IMAGE}:latest"
                    }
                }
            }
    
        }
}