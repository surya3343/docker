pipeline {
    agent {
        label 'master'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }
    
    stages {
        step('Build image') {
            app = docker.build("searce-playground/surya-wordpress")
}
        step('Push image') {
            docker.withRegistry('https://us.gcr.io', 'gcr:searce-playground') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
  }
        }

}
}
