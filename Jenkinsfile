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
        stage('Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'dbe3ba17-2fe3-4eb9-96a1-c9002539cda7', path: '', url: 'http://172.31.30.254:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('Testing')
        {
            steps
            {
                git 'https://github.com/Manojkumar95426/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'dbe3ba17-2fe3-4eb9-96a1-c9002539cda7', path: '', url: 'http://172.31.21.126:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
} 
