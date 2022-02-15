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
                        sh 'sudo chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
                }
            }
            // steps{
            //     script{
            //         withSonarQubeEnv(credentialsId: 'sonar-token') {
            //                 sh 'chmod +x gradlew.bat'
            //                 sh './gradlew sonarqube'
            //         }

            //         timeout(time: 1, unit: 'HOURS') {
            //           def qg = waitForQualityGate()
            //           if (qg.status != 'OK') {
            //                error "Pipeline aborted due to quality gate failure: ${qg.status}"
            //           }
            //         }

            //     }
            // }
        }
    }
    post{
        always{
            echo "EXITO"
        }
    }
}