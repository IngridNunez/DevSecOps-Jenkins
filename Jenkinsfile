pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                    python3 -m venv .venv
                    .venv/bin/pip install -q -r requirements.txt pytest
                '''
            }
        }
        stage('Seguridad') {

          steps {
        
            sh 'bandit -ll app.py'#auditor de seguridad basica 
        
            sh 'pip-audit -r requirements.txt'#para evitar subir una app con elementos vulnerables dentro de una librería
        
          }
        
        }

        stage('Test') {
            steps {
                sh '.venv/bin/python -m pytest -q'
            }
        }

        stage('Deploy') {
            steps {
                sh 'bash deploy.sh'
            }
        }
    }
}
