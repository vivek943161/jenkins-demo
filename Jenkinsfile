pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Script') {
            steps {
                sh 'chmod +x build.sh'
                sh './build.sh'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully'
        }

        failure {
            echo 'Build failed'
        }

        always {
            archiveArtifacts artifacts: 'build.sh', fingerprint: true
        }
    }
}