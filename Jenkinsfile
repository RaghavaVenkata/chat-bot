pipeline {
    environment {
        registry = "venkata7777/chat_bot:latest"
        registryCredential = 'Dockerhub'
        dockerImage = ''
    }
		agent any 
    stages {
        stage('Git Pull') {
            steps {
                git url: 'https://github.com/RaghavaVenkata/chat-bot.git', branch: 'master', credentialsId: 'jenkins_demo'
            }
        }
        stage('Building Image') {
            steps {
                script {
                    dockerImage = docker.build(registry, "./")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Ansible Deploy') {
            steps {
                ansiblePlaybook colorized: true, disableHostKeyChecking: true, installation: 'Ansible', playbook: 'playbook.yml'
            }
        }
    }
}