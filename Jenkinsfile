pipeline {
    agent any

    environment {
        registry = "adesinna/flaskapp"
        registryCredential = 'dockerhub'
    }

    stages {
        stage('Build App Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:V${BUILD_NUMBER}")
                }
            }
        }

        stage('Upload Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push("V${BUILD_NUMBER}")
                        dockerImage.push('latest')
                    }
                }
            }
        }

        stage('Remove Unused Docker Image') {
            steps {
                sh "docker rmi ${registry}:V${BUILD_NUMBER}"
            }
        }
    }
}
