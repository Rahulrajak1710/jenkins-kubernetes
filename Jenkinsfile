pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Rahulrajak1710/jenkins-kubernetes.git']]])
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t rahulrajak/jenkins-kubernetes:latest .'
                }
            }
        }

        stage('Push Docker Image to Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPass', usernameVariable: 'dockerHubUser')]) {
                    script {
                        sh 'docker login -u ${dockerHubUser} -p ${dockerHubPass}'
                        sh 'docker push ${dockerHubUser}/jenkins-kubernetes:latest'
                    }
                }
            }
        }

        stage('Deploy Application on Kubernetes') {
            steps {
                kubernetesDeploy (configs: 'nodejsapp.yaml',kubeconfigId: 'k8sconfigpwd') // k8sconfigpwd is config file 
            }
        }
    }
}

