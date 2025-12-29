pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Manojkumar95426/maven-n.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
