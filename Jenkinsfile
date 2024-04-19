pipeline {
    agent any
    stages {
        stage('Jenkins Discovery') {
            steps {
                echo 'Discovery'
            }
        }
        stage('Build') { 
            steps {
                sh 'mvn clean package'
            }
        }  
        stage('Build Image'){
            steps {
                script {
                    discovery = docker.build("alemagno10/discovery:${env.BUILD_ID}", "-f Dockerfile .")
                }
            }
        }    
        stage('Push Image'){
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        discovery.push("${env.BUILD_ID}")
                        discovery.push("latest")
                    }
                }
            }
        }
    }
}