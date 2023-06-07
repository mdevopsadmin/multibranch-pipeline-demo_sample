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
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/mdevopsadmin/NETFrameworkSample.git']]
                ])
            }
        }

        stage(' Unit Testing') {
            steps {
                
                echo "Running Unit Tests"
               
            }
        }

        stage('Code Analysis') {
            steps {
               
                echo "Running Code Analysis"
              
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                
                echo "Building Artifact"
               

             
                echo "Deploying Code"
               
            }
        }

    }   
}
