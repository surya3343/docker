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
                app = docker.build("searce-playground/surya-wordpress")
                }
        }
        stage ('Push image') {
            step {
                docker.withRegistry('https://us.gcr.io', 'gcr:searce-playground') {
                app.push("${env.BUILD_NUMBER}")
                app.push("latest")
                }
            }
        }
    }
}
