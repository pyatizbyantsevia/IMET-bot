pipeline {
    agent any

    environment {
        TOKEN = credentials('TOKEN')
        MONGO_PWD = credentials('MONGO_PWD')
        PDATA = '/data'
    }
    
    stages {
        stage('Build') {
            steps {
                sh "mkdir -p ${PDATA}"
                sh "rm -rf ${PDATA}/init"
                sh "mv ./mongo/init ${PDATA}/init"
                sh "make docker-build"
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose down'
                sh 'make docker-compose-up'
            }
        }
    }
}
