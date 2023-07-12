pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SunilWork/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    bat 'docker build -t writetosunilinuk/devops-integration .'
                }
            }
        }
        stage('push docker image to hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker-hub-pwd', variable: 'dockerHubPwd')]) {
                        bat 'docker push writetosunilinuk/devops-integration'
}

                }
            }

        }

    }

}