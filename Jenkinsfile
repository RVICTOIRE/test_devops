pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Msdev224/devops_project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m venv venv'
            }
        }

        stage('Run Script') {
            steps {
                bat '.\\venv\\bin\\python app.py'
            }
        }
    }

    post {
        success {
            emailext(
                subject: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Le build de ${env.JOB_NAME} a réussi.\nConsultez les logs ici: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'Rabysene17@gmail.com'
            )
        }

        failure {
            emailext(
                subject: "Build FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Le build de ${env.JOB_NAME} a échoué.\nConsultez les logs ici: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'Rabysene17@gmail.com'
            )
        }
    }
}
