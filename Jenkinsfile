pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
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

        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                script {
                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '',
                file: 'target/VinayDevOpsLab-0.0.12-SNAPSHOT.war', 
                type: 'war']], 
                credentialsId: '2f12efc6-f486-400f-80c2-d3b86dedb8be', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.215:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'RaulRyesDevOpsLab-SNAPSHOT', 
                version: "${Version}"
             }
            }
        }

        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }

        //Stage 5 Deploying 
        stage ('Deploy'){
            steps{
                echo 'Deploying.....'
            }
        }

    }

}