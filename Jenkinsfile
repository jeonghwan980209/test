pipeline {
    agent any
    stages {
        stage('git scm update') {
            steps {
                git url: 'https://github.com/jeonghwan980209/keduitargo.git', branch: 'master'
            }
        }
        stage('docker build and push') {
            steps {
                sh '''
                sudo docker build -t jeonghwan98/keduitlab1:purple .
                sudo docker push jeonghwan98/keduitlab1:purple
                '''
            }
        }
        stage('deploy and service') {
            steps {
                sh '''
                sudo kubectl apply -f deploy.yml
                '''
            }
        }
    }
}
