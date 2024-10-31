pipeline {
    agent any
    stages {
        stage('git scm update') {
            steps {
                git url: 'https://github.com/jeonghwan980209/test.git', branch: 'master'
            }
        }
        stage('docker build and push') {
            steps {
                sh '''
                sudo docker build -t jeonghwan98/keduitlab1:yellow .
                sudo docker push jeonghwan98/keduitlab1:yellow
                ansible node -m shell -a "sudo docker pull jeonghwan98/keduitlab1:yellow"
                '''
            }
        }

        
        stage('deploy and service') {
            steps {
                sh '''
                ansible node -m shell 'sudo kubectl create deploy jenkinstest1 --rplicas 3 --port=80 --image=jeonghwan98/keduitlab1:yellow'
                ansible node -m shell 'sudo kubectl expose deploy jenkinstest1 --type-LoadBalancer --port=80 --targetport=80 --name=jenkinstest1'
                '''
            }
        }
    }
}
