pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Fr3d7/Prueba-Jenkins.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Compilando proyecto...'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONARQUBE = credentials('sonarqube-token')
            }
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat """
                        sonar-scanner ^
                        -Dsonar.projectKey=Prueba-Jenkins ^
                        -Dsonar.sources=. ^
                        -Dsonar.host.url=http://localhost:9000 ^
                        -Dsonar.login=%SONARQUBE%
                    """
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
