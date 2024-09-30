pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/username/repo.git'
            }
        }
        
        stage('Build') {
            steps {
                // Menjalankan build, misalnya menggunakan Maven atau Gradle
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                // Menjalankan pengujian otomatis
                sh 'mvn test'
            }
        }
    }
    
    post {
        always {
            // Mengirim notifikasi setelah build selesai
            emailext (
                subject: "Build ${currentBuild.fullDisplayName} - ${currentBuild.result}",
                body: "The build ${currentBuild.fullDisplayName} has finished with status: ${currentBuild.result}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
        }
    }
}
