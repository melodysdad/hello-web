pipeline {
    agent any
triggers {
        cron('H */8 * * *') //regular builds
        pollSCM('* * * * *') //polling for changes, here once a minute
    }

    stages {
     stage('Checkout') {
                steps { //Checking out the repo
                    checkout changelog: true, poll: true, scm: [$class: 'GitSCM', branches: [[name: '*/main']],  doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git', url: 'ssh://git@git.giturl.com/test/test.git']]]
                }
            }
        stage('Build') {
            stage('Unit & Integration Tests') {
                        steps {
                            script {
                                try {
                                    sh './gradlew clean bootBuildImage --no-daemon' //run a gradle task
                            }
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