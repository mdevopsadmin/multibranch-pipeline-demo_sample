pipeline {

    agent {
        node {
            label 'master'
        }
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                echo "Cleaned Up Workspace For Project"
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/mdevopsadmin/Bookstore_1.git']]
                ])
            }
        }

        stage(' Code Analysis') {
            steps {
              echo "Running Code Analysis"
              bat 'mvn sonar:sonar -Dsonar.projectKey="abcd" -Dsonar.host.url="http://localhost:9003" -Dsonar.login="97df365415abb7c63a5038a2cbe49bd00ed0335d"'
                
                
            }
        }

        stage('Unit Testing') {
            steps {
                echo "Running Unit Tests"
                bat 'mvn clean test'
                
                
            }
        }

        stage('Package Code') {
            
            steps {
                bat 'mvn clean install package'
                
                echo "Building Artifact"
                
            }
        }

    }   
}
