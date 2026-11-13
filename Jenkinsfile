pipeline {
    agent any
    options{
        timestamps()
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'source code downloaded successfully'
            }
        }
        stage('Build') {
            steps {
                echo 'building'
                sh 'python3 -m py_compile app.py'
            }
        }
        stage('Test') {
            steps {
                echo 'running unit tests'
                sh 'python3 -m unittest -v'
            }
        stage('Package') {
            steps {
                echo 'creating application image'
                sh 'tar -czf "python-app-${BUILD_NUMBER}.tar.gz" app.py test_app.py'
                archiveArtifacts artifacts: 'python-app-*.tar.gz', fingerprint:true
            }
        }
    }
    post{
        success{
            echo 'pipeline done'

        failure            echo 'failed'
       }
        always{
           echo 'pipeline execution done'
       }
    }
}
