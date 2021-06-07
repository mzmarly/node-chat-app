pipeline {
    agent any

    tools { nodejs "node"}

    stages {
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'npm install'
                sh 'npm test'
            }
        }
    }
    post {
        failure {
            echo 'Success'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                subject: "Build failed in Jenkins",
                to: 'michalzma@gmail.com'

        }
        success {
            echo 'Fail'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                subject: "Successful build in Jenkins",
                to: 'michalzma@gmail.com'
        }
    }
}
