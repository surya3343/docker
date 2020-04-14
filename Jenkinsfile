pipeline {
    agent {
        label 'master'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }
    environment {
        REGISTRY = 'gcr.io/surya-wordpress'
        IMAGE = 'gcr.io/heptio-images/java'
    }
    stages {
        
        stage('Build image') {
            steps {
                sh("cd discovery && VERSION=${imageVersion} make container")
            }
        }
        stage('Push image') {
            options {
                timeout(time: 10, unit: 'MINUTES')
            }
            steps {
                withCredentials([file(credentialsId: 'heptio-images-gcr', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                    sh("docker push ${imageName}:${imageVersion}")
                }
            }
        }
    }
}
