pipeline {
    agent { label 'dev-agent' }
    
    stages {
        stage('Code') {
            steps {
                git url:'https://github.com/padmalakum/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test') {
            steps {
                sh 'docker build . -t padma0905/node-todo-app:latest'
            }
        }
        stage('docker login and push') {
            steps {
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push padma0905/node-todo-app:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose down && docker-compose up -d --no-deps --build web'
            }
        }
}    
}
