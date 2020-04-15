pipeline {
    agent {
        label 'master'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }

    environment {
        tag = '${BUILD_NUMBER}'

    }
    
    stages {
        stage ('Build image') {
            steps {
                script{
                Image = docker.build("searce-playground/surya-wordpress")
                }
            }
        }
        stage ('Push image') {
            steps {
                script {
                    docker.withRegistry('https://us.gcr.io', 'gcr:searce-playground') {
                        Image.push(tag)
                    }
                }
                
            }
        }
    }
}
