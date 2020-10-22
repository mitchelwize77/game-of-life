pipeline

  agent { label 'HRMS&&QA' }
  triggers { cron('50 * * * 1-2') }

  stages {
      stage ('git') {
          steps {
              git 'https://github.com/mitchelwize77/game-of-life'
          }
      }
      stage ('build') {
          steps {
              sh 'mvn clean package'
          }
      }
      stage ('TestReports') {
          steps {
              junit 'gameoflife-web/target/surefire-reports/*.xml'
          }
      }  

  }

    