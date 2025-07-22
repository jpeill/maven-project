pipeline {
    agent any  
    environment{
        NAME = "jeremy"
    }
    parameters {
        string defaultValue: 'peilleron', name: 'LASTNAME'
    }

    tools {
        maven 'mymaven'
    }

    stages{
        stage('build stage'){
            steps{
                bat 'mvn clean package'
                echo "hello $NAME ${params.LASTNAME}"
            }

            post {
                success {
                   archiveArtifacts artifacts: '**/target/*.war'
                }
            }

        }
    } 
}
