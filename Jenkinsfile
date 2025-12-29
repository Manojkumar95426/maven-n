pipeline {
    agent any
    
    stages {
        stage('ContinuousDownload') {
            steps {
                // Main application source code
                git 'https://github.com/Manojkumar95426/maven-n.git' 
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        
        stage('Deployment') {
            steps {
                // Deploying to Test environment
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'dbe3ba17-2fe3-4eb9-96a1-c9002539cda7', path: '', url: 'http://172.31.30.254:8080')], 
                       contextPath: 'testapp', 
                       war: 'target/*.war'
            }
        }
        
        stage('Testing') {
            steps {
                // Use dir() to download testing tools into a sub-folder
                dir('test-scripts') {
                    git 'https://github.com/Manojkumar95426/FunctionalTesting.git'
                }
                // Run the jar using a relative path to keep it portable
                sh 'java -jar test-scripts/testing.jar'
            }
        }
        
        stage('Delivery') {
            steps {
                // Deploying to Production environment
                // This will now work because 'target/*.war' was not deleted by the git command
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'dbe3ba17-2fe3-4eb9-96a1-c9002539cda7', path: '', url: 'http://172.31.21.126:8080')], 
                       contextPath: 'prodapp', 
                       war: 'target/*.war'
            }
        }
    }
}
