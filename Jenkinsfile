pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/thisismikem/myapp.git'
            }
        }
        
    }
}