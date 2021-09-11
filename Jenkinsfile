pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName
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
        //Stage3: Publis the artifacts to Nexus
        stage('Publish to Nexus'){
            steps{
            nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.12-SNAPSHOT.war', type: 'war']], credentialsId: '2f12efc6-f486-400f-80c2-d3b86dedb8be', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.215:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'RaulRyesDevOpsLab-SNAPSHOT', version: '0.0.12-SNAPSHOT'
            }
        }
        // Stage 4 : Print some informacion
        stage ('Print Enviroment Variables'){
            steps{
                echo "Artifact ID is ${ArtifactId}"
                echo "Version is ${Version}"
                echo "GroupID is ${}"
                echo "Name is ${Name}"
            }
        }

        // Stage3 : Deploying
        stage ('Deploying'){
            steps {
                echo ' deploying......'
            }
        }

        
        
    }

}