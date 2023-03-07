pipeline{
    //Directives
    agent any
    tools {
        maven 'maven3'
    }
    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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
                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'd4ccc5a3-0ed9-417a-90e5-55e25ac684e4', 
                groupId: "${GroupId}", 
                nexusUrl: '172.31.37.64:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'AnandDevOpsLab-SNAPSHOT', 
                version: "${Version}"
            }
        }

        // Stage3 : Publish the source code to Sonarqube
     /*  stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }

            }
        }*/

        
        
    }

}
