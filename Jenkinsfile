pipeline {
    agent any
    
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
            sh '''
            SLACK_URL="https://hooks.slack.com/services/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"
            PAYLOAD='{"text":"✅ Build #'${BUILD_NUMBER}' SUCCESS - Amazon-Jenkins"}'
            curl -X POST -H "Content-type: application/json" -d "$PAYLOAD" "$SLACK_URL"
            '''
        }
        failure{
            echo 'Failure in the build'
            sh '''
            SLACK_URL="https://hooks.slack.com/services/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"
            PAYLOAD='{"text":"❌ Build #'${BUILD_NUMBER}' FAILED - Amazon-Jenkins"}'
            curl -X POST -H "Content-type: application/json" -d "$PAYLOAD" "$SLACK_URL"
            '''
        }
    }
}
