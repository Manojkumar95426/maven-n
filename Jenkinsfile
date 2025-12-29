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

        stage('Deployment') {
            steps {
                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'd3058440-8aa0-40d7-9658-695a699b868d',
                        path: '',
                        url: 'http://172.31.30.254:8080'
                    )
                ],
                contextPath: 'testapp1',
                war: '**/*.war'
            }
        }

        stage('Testing') {
            steps {
                git 'https://github.com/Manojkumar95426/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/dp-2/testing.jar'
            }
        }

        stage('Delivery') {
            steps {
                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'd3058440-8aa0-40d7-9658-695a699b868d',
                        path: '',
                        url: 'http://172.31.21.126:8080'
                    )
                ],
                contextPath: 'app1',
                war: '**/*.war'
            }
        }

    }
}
