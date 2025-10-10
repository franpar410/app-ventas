pipeline {
    agent any
    
    triggers {
        pollSCM('H/2 * * * *')
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/franpar410/app-ventas.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt || echo "No requirements.txt"'
            }
        }

        stage('Build') {
            steps {
                echo 'Este es un build de prueba'
                sh 'echo "Hola desde Jenkins!"'
            }
        }

        stage('Push to Registry (optional)') {
            when {
                expression { return false }
            }
            steps {
                sh 'echo "Pushing to Docker Registry..."'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploying to environment..."'
            }
        }
    }
}
