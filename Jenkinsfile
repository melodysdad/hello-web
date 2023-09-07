pipeline {
    agent any
triggers {
        pollSCM('* * * * *') //polling for changes, here once a minute
    }

    stages {
     stage('Checkout') {
        steps { //Checking out the repo
            checkout changelog: true, poll: true, scm: [$class: 'GitSCM', branches: [[name: '*/main']],  doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git', url: 'ssh://git@git.giturl.com/test/test.git']]]
        }
     }
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