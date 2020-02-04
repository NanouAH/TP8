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
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build', body: 'message', from: 'jenkins-notification@jenkins.com', to: 'gn_ahmim@esi.dz')
      }
    }

    stage('Code analysis') {
      parallel {
        stage('Code analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube'
            }

            waitForQualityGate true
          }
        }

        stage('Test Reporting') {
          steps {
            jacoco(exclusionPattern: '**/test/*.class', execPattern: 'build/jacoco/*.exec')
          }
        }

      }
    }

    stage('Deployment') {
      when {branch'master'}
      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack Notification') {
        when {branch'master'}
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', token: 'TRQR5NKUM/BT54Q7NV8/WnnX2tVffqGr6gUUuZ0j9AGm', message: 'Notification', teamDomain: 'esi-mmt2501', channel: 'général')
      }
    }

  }
}
