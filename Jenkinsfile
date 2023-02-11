pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean'
                sh 'mvn install'
                sh 'mvn package'
            }
        }
        stage('upload artifact') {
            steps {
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                 nexusArtifactUploader artifacts: 
                 [[artifactId: '${POM_ARTIFACTID}',
                  classifier: '', 
                  file: 'target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}', 
                  type: '${POM_PACKAGING}']], 
                  credentialsId: 'NexusID', 
                  groupId: '${POM_GROUPID}', 
                  nexusUrl: '192.168.50.10:8081', 
                  nexusVersion: 'nexus3', 
                  protocol: 'http', 
                  repository: 'biomedical_app_repo', 
                  version: '${POM_VERSION}'
                }
            }
        }


