pipeline {
    agent any
    environment {
        GIT_URL = 'https://github.com/ahmadilmannafia7/pandawa-project-1'
        BRANCH_NAME = 'main'  // Sesuaikan dengan branch yang Anda gunakan
    }
    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Pastikan Git sudah terinstall dan dapat digunakan di Windows
                    sh 'git config --global core.autocrlf input'
                    sh 'git config --global user.name "Your Name"'
                    sh 'git config --global user.email "your-email@example.com"'
                    git url: GIT_URL, branch: BRANCH_NAME
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Running Build Process...'
                    // Sesuaikan dengan perintah build yang Anda perlukan
                    bat 'echo Building...'
                }
            }
        }

          stage('Docker Image Creation') {
            steps {
                script {
                    echo 'Creating Docker Image...'
                    // Pastikan build dilakukan di direktori yang sesuai dengan Dockerfile
                    bat 'docker build -f Dockerfile -t myapp .'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying Application...'
                    // Perintah untuk deployment aplikasi Anda
                    bat 'docker run -d -p 8080:80 myapp'
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            cleanWs()  // Membersihkan workspace Jenkins setelah pipeline selesai
        }
        failure {
            echo 'Pipeline Failed. Please check the logs!'
        }
    }
}
