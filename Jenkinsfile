pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x build.sh'
                sh './build.sh'
            }
        }
    }

    post {

        success {
            emailext(
                to: 'vivekrj62@gmail.com',
                subject: "SUCCESS: Jenkins Build #${BUILD_NUMBER}",
                body: """
Build completed successfully.

Job: ${JOB_NAME}
Build Number: ${BUILD_NUMBER}
Build URL: ${BUILD_URL}

Git Commit:
${GIT_COMMIT}

Please see the attached Jenkins console output.
""",
                attachLog: true
            )
        }

        failure {
            emailext(
                to: 'vivekrj62@gmail.com',
                subject: "FAILED: Jenkins Build #${BUILD_NUMBER}",
                body: """
Jenkins build failed.

Job: ${JOB_NAME}
Build Number: ${BUILD_NUMBER}
Build URL: ${BUILD_URL}

Please check the attached console output.
""",
                attachLog: true
            )
        }
    }
}