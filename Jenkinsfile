def COLOR_MAP = ['SUCCESS': 'good', 'FAILURE': 'danger', 'UNSTABLE': 'danger', 'ABORTED': 'danger']
def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}
pipeline {
    agent any
 environment {
        BUILD_USER = ''
       }
    stages {
        stage('Build') {
            steps {
                script {
                    BUILD_USER = getBuildUser()
                }
                slackSend channel: '#jenkins-pipeline-demo',
                   color: COLOR_MAP[currentBuild.currentResult],
                    message: "${env.JOB_NAME} - #${env.BUILD_NUMBER} STARTED by ${BUILD_USER}\n More info at: ${env.BUILD_URL}"
 
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
               echo 'Deploying....'
            }
        }
    }
    
    post {
        always {
           
    script {
                    BUILD_USER = getBuildUser()
                }
         
         slackSend channel: '#jenkins-pipeline-demo',
                   color: COLOR_MAP[currentBuild.currentResult],
                    message: "${env.JOB_NAME} - #${env.BUILD_NUMBER} ${currentBuild.currentResult} after ${currentBuild.durationString}\n More info at: ${env.BUILD_URL}"
            
    }
    }
}
