pipeline {
    agent any
        tools{
        nodejs 'NodeJS'
    }
    stages {
            stage('clone repository') {
      steps { 
        git 'https://github.com/Emmanuel-Mose/gallery.git'
      }
    }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

    stage('Test') {
      steps {
         sh 'npm test'
      }
}
        stage('Deploy to Render') {
            steps {
                sh 'npm start &'
                sh 'sleep 10'
                sh 'curl -sSf http://localhost:8000 || exit 1'
            }
        
        }
    }
}
    post{
        always{
            slackSend( channel: "#jenkins", token: "slack_webhook token", color: "good", message: "NodeJS gallery Pipeline Message- ${currentBuild.currentResult}  ${env.JOB_NAME} ${env.BUILD_NUMBER} ${BUILD_URL}")
        }
    }
