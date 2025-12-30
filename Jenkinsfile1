pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/Manojkumar95426/maven-n.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '02f8f132-1fe0-4d6d-bdd7-ba9d9aca0c0b', path: '', url: 'http://172.31.24.193:8080')], contextPath: 'teatapp', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/Manojkumar95426/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '02f8f132-1fe0-4d6d-bdd7-ba9d9aca0c0b', path: '', url: 'http://172.31.20.203:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
