pipeline {

        agent any

        environment {
        
            DOCKER_REGISTRY = 'https://index.docker.io/v1/'
            DOCKER_IMAGE = 'reshmastani382/xyzimage'

        }
        tools {
            maven 'mymaven'
        }
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
                    withDockerRegistry(credentialsId: '5bf62ccb-3ee7-415b-9e5a-cbd3f5266763', url: DOCKER_REGISTRY) {
                        sh "docker push ${DOCKER_IMAGE}:latest"
                    }
                }
            }
    
        }
}