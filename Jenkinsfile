pipeline {
    agent any

    stages {

        stage('ContinuousDownload') {
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
                        credentialsId: 'tomcat-creds',
                        path: '',
                        url: 'http://172.31.30.254:8080'
                    )
                ],
                contextPath: 'testapp1',
                war: 'webapp/target/webapp.war'
            }
        }

        stage('Testing') {
            steps {
                git 'https://github.com/Manojkumar95426/FunctionalTesting.git'
                sh 'java -jar testing.jar'
            }
        }

        stage('Delivery') {
            steps {
                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'tomcat-creds',
                        path: '',
                        url: 'http://172.31.21.126:8080'
                    )
                ],
                contextPath: 'app1',
                war: 'webapp/target/webapp.war'
            }
        }
    }
}
