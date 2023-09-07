pipeline {
    agent any
triggers {
        pollSCM('* * * * *') //polling for changes, here once a minute
    }

    stages {

     stage('Build') {
        steps {
            script {
                sh './gradlew clean bootBuildImage --no-daemon' //run a gradle task
            }
        }
     }
     stage('Deploy') {
        steps {
            echo 'Deploying....'
        }
     }
    }
}