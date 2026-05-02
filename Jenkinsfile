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
            curl -X POST -H 'Content-type: application/json' \
            --data '{"text":"✅ Build #${BUILD_NUMBER} SUCCESS - Amazon-Jenkins"}' \
            https://hooks.slack.com/services/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
            '''
        }
        failure{
            echo 'Failure in the build'
            sh '''
            curl -X POST -H 'Content-type: application/json' \
            --data '{"text":"❌ Build #${BUILD_NUMBER} FAILED - Amazon-Jenkins"}' \
            https://hooks.slack.com/services/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
            '''
        }
    }
}
