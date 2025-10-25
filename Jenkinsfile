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
                        // Obtiene la ruta del sonar-scanner que definiste en Global Tool Configuration
                        def scannerHome = tool 'sonar-scanner-win'

                        bat """
                        "${scannerHome}\\bin\\sonar-scanner.bat" ^
                          -Dsonar.projectKey=Prueba-Jenkins ^
                          -Dsonar.sources=. ^
                          -Dsonar.host.url=http://localhost:9000 ^
                          -Dsonar.login=${env.squ_c892ec834c9f1e88d89747a907469cc89088e91d}
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
