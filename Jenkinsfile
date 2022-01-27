pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
        
        stage ('publish to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.2-SNAPSHOT.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.vinaysdevopslab', nexusUrl: '172.31.10.168:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'ananddevops-snapshot', version: '0.0.2-SNAPSHOT'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
     /*   stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }

            }
        }*/

        
        
    }

}
