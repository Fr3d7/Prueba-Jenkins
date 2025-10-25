pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-local') {
                    script {
                        // 1. Pedirle a Jenkins la ruta del scanner que configuraste como "sonar-scanner-win"
                        def scannerHome = tool 'sonar-scanner-win'

                        // 2. Ejecutar el scanner con bat en Windows
                        bat """
                            "${scannerHome}\\bin\\sonar-scanner.bat" ^
                              -Dsonar.projectKey=Prueba-Jenkins ^
                              -Dsonar.sources=. ^
                              -Dsonar.host.url=http://localhost:9000 ^
                              -Dsonar.login=squ_c892ec834c9f1e88d89747a907469cc8908e891d
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminado'
        }
    }
}
