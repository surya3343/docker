pipeline {
    agent {
        label 'master'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }
    environment {
        REGISTRY = 'us.gcr.io/surya-wordpress'
        IMAGE = 'us.gcr.io/surya-wordpress/java'

    }
    stages {
        stage('Determine version') {
            steps {
                script {
                    if (env.BRANCH_NAME == "master") {
                        imageRepo = env.REGISTRY
                        imageName = env.IMAGE

                    } else if (env.BRANCH_NAME ==~ /PR-[0-9]+/) {
                        imageRepo = env.REGISTRY
                        imageName = env.IMAGE

                    }
                }
            }
        }
        stage('Build image') {
            steps {
                sh("docker build ${imageName}")
            }
        }
        stage('Push image') {
            options {
                timeout(time: 10, unit: 'MINUTES')
            }
            steps {
                withCredentials([file(credentialsId: '	searce-playground', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                    sh("docker push ${imageName}")
                }
            }
        }
    }
}
