pipeline {
    agent {
        docker { image 'openjdk:17.0.2' }
    }
    stages {
        stage('Build with unit testing') {
            steps {
                echo 'Building...' + env.BRANCH_NAME
            }
        }
        stage('Security Stage') {
            steps {
                echo "Testing security with snyk"
            }
        }
        stage('Code coverage Test') {
            steps {
                echo "Todo install sonarqube server"
            }
        }
        stage("Test stage") {
            steps {
                sh "./mvnw test"
            }
        }
        stage("Build") {
            steps {
                sh "./mvnw compile"
            }
        }
        
    }
}
post {
success {
office365ConnectorSend color: '#86BC25', status: currentBuild.result, webhookUrl: "https://jalauniv.webhook.office.com/webhookb2/16615a8a-24bc-4fcf-9533-ccf7e583282e@e342d848-a6cb-46aa-ac19-4800f62fb836/IncomingWebhook/dc2e60298e144cd8bfd2dc90ac57c1af/7b849e04-cb75-4a3d-9ead-99e784324c15",
message: "Test Successful: ${JOB_NAME} - ${currentBuild.displayName}<br>Pipeline duration: ${currentBuild.durationString.replace(' and counting', '')}"
}
unstable {
   office365ConnectorSend color: '#FFE933', status: currentBuild.result, webhookUrl: "https://jalauniv.webhook.office.com/webhookb2/16615a8a-24bc-4fcf-9533-ccf7e583282e@e342d848-a6cb-46aa-ac19-4800f62fb836/IncomingWebhook/dc2e60298e144cd8bfd2dc90ac57c1af/7b849e04-cb75-4a3d-9ead-99e784324c15",
   message: "Successfully Build but Unstable. Unstable means test failure, code violation, push to remote failed etc. : ${JOB_NAME} - ${currentBuild.displayName}<br>Pipeline duration: ${currentBuild.durationString.replace(' and counting', '')}"
  }
failure {
office365ConnectorSend color: '#ff0000', status: currentBuild.result, webhookUrl: "https://jalauniv.webhook.office.com/webhookb2/16615a8a-24bc-4fcf-9533-ccf7e583282e@e342d848-a6cb-46aa-ac19-4800f62fb836/IncomingWebhook/dc2e60298e144cd8bfd2dc90ac57c1af/7b849e04-cb75-4a3d-9ead-99e784324c15",
message: "Build Failed: ${JOB_NAME} - ${currentBuild.displayName}<br>Pipeline duration: ${currentBuild.durationString.replace(' and counting', '')}"
}
always {
echo "Build completed with status: ${currentBuild.result}"
}
}

