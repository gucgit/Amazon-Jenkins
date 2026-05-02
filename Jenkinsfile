pipeline {
    agent any
    environment {
        // Use PATH+EXTRA to append to PATH properly
        PATH = "/usr/bin:/bin:/opt/homebrew/bin"
        SLACK_WEBHOOK = "https://hooks.slack.com/services/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"
    }
    stages {
        stage('pull scm git ') {
            steps {
                git branch: 'main', url: 'https://github.com/gucgit/Amazon-Jenkins.git'
            }
        }
        stage('compile ') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('build') {
            steps {
                 sh 'mvn clean install'
            }
        }
        
    }
    post{
        success{
            echo 'Build success 1'
            script {
                sh '''
                curl -X POST \
                  -H 'Content-type: application/json' \
                  --data '{"text":"✅ Jenkins Build #${BUILD_NUMBER} SUCCESS","attachments":[{"color":"#36a64f","fields":[{"title":"Job","value":"Amazon-Jenkins","short":true},{"title":"Build #","value":"${BUILD_NUMBER}","short":true},{"title":"Branch","value":"main","short":true},{"title":"Status","value":"SUCCESS","short":true}]}]}' \
                  ${SLACK_WEBHOOK}
                '''
            }
        }
        failure{
            echo 'Failure in the build'
            script {
                sh '''
                curl -X POST \
                  -H 'Content-type: application/json' \
                  --data '{"text":"❌ Jenkins Build #${BUILD_NUMBER} FAILED","attachments":[{"color":"#dc3545","fields":[{"title":"Job","value":"Amazon-Jenkins","short":true},{"title":"Build #","value":"${BUILD_NUMBER}","short":true},{"title":"Branch","value":"main","short":true},{"title":"Status","value":"FAILED","short":true}]}]}' \
                  ${SLACK_WEBHOOK}
                '''
            }
        }
    }
}
