pipeline {
    agent any  
    environment{
        NAME = "jeremy"
    }
    parameters {
        choice choices: ['dev', 'prod'], name: 'select_environment'
    }

    tools {
        maven 'mymaven'
    }

    stages{
        stage('build stage'){
            steps{
                bat 'mvn clean package -DskipTests=True'
            }
        }

        stage('test'){
            parallel {
                stage('testA'){
                    agent any
                    steps{
                        echo 'this is test A'
                        bat "mvn test"
                    }
                }
                stage('testB'){
                    agent any
                    steps{
                        echo 'this is test B'
                        bat "mvn test"
                    }
                }
            }
            post {
                success {
                   archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('deploy dev'){
            when { 
                expression {params.select_environment == 'dev'}
                beforeAgent true}
            agent { label 'built-in'}
            steps{
                bat "jar -xvf /webapp/target/webapp.war"
            }
        }

    } 
}
