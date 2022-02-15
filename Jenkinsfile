pipeline{
    agent any
    stages{
        stage("Sonar quality check"){
            agent{
                docker{
                    image 'openjdk:11'
                }
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'Mi-Sonar-Admin-Token') {
                        sh 'chmod +x gradlew.bat'
                        sh './gradlew sonarqube'
                    }
                }
            }
        }
    }
    post{
        always{
            echo "EXITO"
        }
    }
}