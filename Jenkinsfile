pipeline {
    agent any
    
    tools {
        maven 'mymaven'
    }

    stages{
        stage('build stage'){
            steps{
                bat 'mvn clean package'
            }

            post {
                success {
                   archiveArtifacts artifacts: '**/target/*.jar'
                }
            }

        }
    } 
}
