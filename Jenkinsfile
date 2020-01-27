pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'C:\\Users\\Latitude\\Desktop\\gradle-6.0.1\\bin\\gradle build'
        bat 'C:\\Users\\Latitude\\Desktop\\gradle-6.0.1\\bin\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc'
      }
    }

  }
}