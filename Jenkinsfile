def message =""
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'C:\\Users\\Latitude\\Desktop\\gradle-6.0.1\\bin\\gradle build'
        bat 'C:\\Users\\Latitude\\Desktop\\gradle-6.0.1\\bin\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
        junit 'build\\test-results\\test\\*.xml'
      }
    
    post{
      always { echo "Build Stage Complete"}
      failure {script{message= "Build failed"}}
      success {script{message="Build succeeded"}}
    }
                 

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build', body: "${message}", from: 'jenkins-notification@jenkins.com', to: 'gn_ahmim@esi.dz')
      }
    } 

    }}

