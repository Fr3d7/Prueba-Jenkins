pipeline {
    agent any

    environment {
        // nombre EXACTO del server configurado en Manage Jenkins > System > SonarQube servers
        SONARQUBE_SERVER = 'sonar-local'

        // id EXACTO de la credencial tipo "Secret text" con tu token de SonarQube
        SONAR_TOKEN_CRED = 'sonarqube-token'

        // url de tu sonarqube
        SONAR_HOST_URL   = 'http://localhost:9000'

        // clave del proyecto en sonarqube
        SONAR_PROJECT_KEY = 'Prueba-Jenkins'
    }

    stages {

        stage('Checkout') {
            steps {
                // usa la config SCM que ya tiene tu job (tu repo GitHub)
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // esto carga en variables de entorno (como SONAR_HOST_URL) la config del servidor "sonar-local"
                withSonarQubeEnv("${SONARQUBE_SERVER}") {

                    // esto saca tu token secreto de Jenkins Credentials y lo pone en la var SONAR_LOGIN
                    withCredentials([string(credentialsId: "${SONAR_TOKEN_CRED}", variable: 'SONAR_LOGIN')]) {

                        script {
                            // "scanner-cli" DEBE ser el mismo nombre que le diste en
                            // Manage Jenkins > Tools > SonarQube Scanner (Name)
                            def scannerHome = tool 'scanner-cli'

                            // en Windows usamos bat y llamamos sonar-scanner.bat
                            bat """
                                "${scannerHome}\\bin\\sonar-scanner.bat" ^
                                  -Dsonar.projectKey=${SONAR_PROJECT_KEY} ^
                                  -Dsonar.sources=. ^
                                  -Dsonar.host.url=${SONAR_HOST_URL} ^
                                  -Dsonar.login=%SONAR_LOGIN%
                            """
                        }
                    }
                }
            }
        }

        stage('Fin') {
            steps {
                echo 'Pipeline terminado ✅'
            }
        }
    }

    post {
        always {
            echo 'Listo. Esto fue una prueba con SonarQube.'
        }
    }
}
