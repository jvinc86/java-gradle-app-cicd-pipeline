pipeline{
    agent any
    stages{
        stage("Sonar quality check"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'Mi-Sonar-Admin-Token') {
                        sh 'sudo chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
                    timeout(time: 5, unit: 'MINUTES') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') { error "Pipeline fue abortado debido a una falla en quality gate: ${qg.status}" }
                    }
                }
            }
        }
    }
    // post{
    //     always{
    //         echo "EXITO"
    //     }
    // }
}
