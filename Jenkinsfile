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
                        // 1. obtiene la ruta real al scanner que definiste como sonar-scanner-win
                        def scannerHome = tool 'sonar-scanner-win'

                        // 2. usa el token que guardaste en Jenkins como credencial tipo "Secret text"
                        withCredentials([string(credentialsId: 'sonarqube-token', variable: 'squ_c892ec834c9f1e88d89747a907469cc89088e91d')]) {

                            bat """
                            "${scannerHome}\\bin\\sonar-scanner.bat" ^
                              -Dsonar.projectKey=Prueba-Jenkins ^
                              -Dsonar.sources=. ^
                              -Dsonar.host.url=http://localhost:9000 ^
                              -Dsonar.login=%squ_c892ec834c9f1e88d89747a907469cc89088e91d%
                            """
                        }
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
