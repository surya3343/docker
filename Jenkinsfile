pipeline {
    agent {
        label 'master'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }
    
    stages {
        stage ('Build image') {
            steps {
                script{
                docker.build("searce-playground/surya-wordpress")
                }
            }
        }
        stage ('Push image') {
            steps {
                script {
                    docker.withRegistry('https://us.gcr.io', 'gcr:searce-playground') {
                        dockerImage.push()
                    }
                }
                
            }
        }
    }
}
