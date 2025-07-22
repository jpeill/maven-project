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
        }

        stage('test'){
            parallel {
                stage('testA'){
                    steps{
                        echo 'this is test A'
                    }
                }
                stage('testB'){
                    steps{
                        echo 'this is test B'
                    }
                }
            }
            post {
                success {
                   archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    } 
}
