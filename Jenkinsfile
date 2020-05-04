pipeline {
    agent any
   tools {
        maven 'Maven3'
    }
   /*  options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }*/
    stages{
        stage('Build'){
            steps{
                // def mvnHome = tool name: 'Maven3', type: 'maven'
                // bat script: "${mvnHome}/bin/mvn clean package"
                 bat script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            } 
        }
        stage('Upload War To Nexus'){
            steps{
                script{

                  /*  def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release" */
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'simple-app', 
                            classifier: '', 
                            file: "target/simple-app-2.0.0.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus3', 
                    groupId: 'in.javahome', 
                    nexusUrl: '10.110.39.220:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'simpleapp-release', 
                    version: "2.0.0"
                    }
            }
        }
    }
}
