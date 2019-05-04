pipeline {
    agent {
        label 'test_node'
    }

    stages {
        stage ('Compile Stage') {

            steps {
               dir ('workspace/Job_pipeline/sonar'){
                  
               
                sh 'bat mvn clean compille'
            }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven') {
                    sh 'mvn test'
                }
            }
        }
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'maven') {
                    sh 'mvn deploy'
                }
            }
        }
        
    }
}

