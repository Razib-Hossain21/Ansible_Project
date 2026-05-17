pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Building..."
            }
        }

        stage('Test') {
            steps {
                echo "Testing..."
            }
        }
    }

    post {

        success {
            emailext(
                to: 'unionins97@gmail.com',
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                mimeType: 'text/html',
                body: """
                <html>
                <body>
                    <h3 style="color:green;">Build SUCCESS</h3>

                    <p>Hello Razib,</p>
                    <p>Your pipeline completed successfully.</p>

                    <table cellpadding="6">
                        <tr><td><b>Job</b></td><td>${env.JOB_NAME}</td></tr>
                        <tr><td><b>Build</b></td><td>${env.BUILD_NUMBER}</td></tr>
                        <tr><td><b>Status</b></td><td style="color:green;"><b>SUCCESS</b></td></tr>
                    </table>

                    <p><a href="${env.BUILD_URL}">View Build</a></p>

                    <p>— Jenkins</p>
                </body>
                </html>
                """
            )
          slackSend(
                channel: 'C0B47RAFKUJ', 
                message: "✅ SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' completed successfully!\n${env.BUILD_URL}",
                color: '#36a64f'
            )
        }

        failure {
            emailext(
                to: 'unionins97@gmail.com',
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                mimeType: 'text/html',
                body: """
                <html>
                <body>
                    <h3 style="color:red;">Build FAILED</h3>

                    <p>Hello Razib,</p>
                    <p>Pipeline execution failed. Please check logs.</p>

                    <table cellpadding="6">
                        <tr><td><b>Job</b></td><td>${env.JOB_NAME}</td></tr>
                        <tr><td><b>Build</b></td><td>${env.BUILD_NUMBER}</td></tr>
                        <tr><td><b>Status</b></td><td style="color:red;"><b>FAILED</b></td></tr>
                    </table>

                    <p><a href="${env.BUILD_URL}">Check Build</a></p>

                    <p>— Jenkins</p>
                </body>
                </html>
                """
            )
	  slackSend(
                channel: 'C0B47RAFKUJ',
                message: "❌ FAILED: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] failed due to configuration error!\n${env.BUILD_URL}",
                color: '#ff0000'
            )
        }
    }
}
