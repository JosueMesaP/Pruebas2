pipeline {
    agent any
    stages {
        
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQubePruebas') {
                    bat "mvn clean verify sonar:sonar"
                }
            }
        }
        stage("Quality gate") {
            steps {
                timeout(time: 2, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        
    }
    post{
            success{
                bat "curl http://PepitoPerez:MamaGu3bo@localhost:8080/job/Tareas3dediciembre/job/DesplegarProduccion/build?token=963852"
                bat "echo Tarea Desplegar en servidor de produccion Iniciada correctamente"
            }
            failure{
                bat "curl http://PepitoPerez:MamaGu3bo@localhost:8080/job/Tareas3dediciembre/job/Notificar/build?token=789456"
                bat "echo Tarea notificar al correo Iniciada correctamente"
            }
        }
}
