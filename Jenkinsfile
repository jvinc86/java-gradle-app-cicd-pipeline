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
        stage("Buildear y obtener .war"){
            steps{
                script{
                    sh './gradlew clean build'
                }
            }
        }
        stage("Docker build y push"){
            steps{
                script{
                    sh 'cd /var/lib/jenkins/workspace/mi_gradle_java_app'
					sh 'docker build -t 13.38.75.173:8083/$JOB_NAME:v$BUILD_NUMBER .'
                    sh 'docker tag 13.38.75.173:8083/$JOB_NAME:v$BUILD_NUMBER 13.38.75.173:8083/$JOB_NAME:latest'

                    sh 'docker login -u admin -p Vinc.3006 13.38.75.173:8083'
                    sh 'docker push 13.38.75.173:8083/$JOB_NAME:v$BUILD_NUMBER'
                    sh 'docker push 13.38.75.173:8083/$JOB_NAME:latest'
                    sh 'docker image rm -f 13.38.75.173:8083/$JOB_NAME:v$BUILD_NUMBER'
                    sh 'docker image rm -f 13.38.75.173:8083/$JOB_NAME:latest'
                }
            }
        }
    }
}
