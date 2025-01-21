pipeline {
    agent any
    options {
        timeout(time: 1, unit: 'MINUTES')
    }
  
    stages {
        stage('Inicio de options') {
            steps {
                echo "El pipeline ejecuta una tarea con un timeout de 1 minutos"
            }
        }
        stage('Tarea por tiempo') {
            steps {
                echo "Empezando simulacion de tarea larga..."
                catchError(buildResult: 'ABORTED', stageResult: 'ABORTED') {
                    echo 'Empezando la actividad de error...'
                    sleep(time: 2, unit: 'MINUTES')
                }
            }
        }

        stage('Finalizando') {
            steps {
                echo "Tarea procesada..."
            }
        }
    }

    post {
        always {
            script {
                if (currentBuild.result == 'ABORTED') {
                    mail to: 'paulgiraldo72@gmail.com',
                         subject: 'Pipeline ejecucion Error',
                         body: "El pipeline ${env.JOB_NAME} con el build numero ${env.BUILD_NUMBER} ha finalizado de manera Incorrecta"
                }
            }
        }
    }
}
