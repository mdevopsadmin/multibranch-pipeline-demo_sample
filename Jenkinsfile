pipeline {

    agent {
        node {
            label 'node1'
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

         stage('Code Analysis') {
            steps {
               
                echo "Running Code Analysis"
              bat 'SonarScanner.MSBuild.exe begin /k:"NET_PROJECT_SONAR_PIPELINE" /d:sonar.host.url="http://localhost:9003" /d:sonar.login="6412c4b1ca12e92b5302cbd8b97e9644781e9174"'
            bat 'MsBuild.exe /t:Rebuild'
                SonarScanner.MSBuild.exe end /d:sonar.login="6412c4b1ca12e92b5302cbd8b97e9644781e9174"
            }
        }
        
        stage(' Package Update') {
            steps {
                
                echo "Running Unit Tests"
               bat '.paket/paket.exe update'
            }
        }
           
        stage(' Package Restore') {
            steps {
                
                echo "Running Unit Tests"
               bat '.paket/paket.exe restore'
            }
        }
        

       

        stage('Build Deploy Code') {
            
            steps {
                
                echo "Building Artifact"
               
            bat 'MsBuild.exe PaketBindingRedirects.sln /t:rebuild'
             
                echo "Deploying Code"
               
            }
        }

    }   
}
