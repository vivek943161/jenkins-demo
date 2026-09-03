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
                sh 'chmod +x hello.sh'
                sh './hello.sh'
            }
        }
    }

    post {

        success {
            emailext(
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Jenkins Build Successful</h2>

                    <p><b>Job:</b> ${env.JOB_NAME}</p>
                    <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                    <p><b>Status:</b> SUCCESS</p>
                    <p><b>Git Commit:</b> ${env.GIT_COMMIT}</p>

                    <h3>Build Output</h3>

                    <p>See the attached Jenkins build log.</p>

                    <p>
                    <a href="${env.BUILD_URL}">
                    Open Jenkins Build
                    </a>
                    </p>
                """,
                to: "vivekrj62@gmail.com",
                attachLog: true
            )
        }

        failure {
            emailext(
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Jenkins Build Failed</h2>

                    <p><b>Job:</b> ${env.JOB_NAME}</p>
                    <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                    <p><b>Status:</b> FAILED</p>

                    <p>
                    <a href="${env.BUILD_URL}">
                    Open Jenkins Build
                    </a>
                    </p>
                """,
                to: "vivekrj62@gmail.com",
                attachLog: true
            )
        }
    }
}
