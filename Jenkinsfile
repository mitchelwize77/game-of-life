node ('HRMS&&QA')

  stage ('git') {

      git 'https://github.com/mitchelwize77/game-of-life'
  }

  stage ('compile') {

      sh 'mvn package'
  }    

  stage ('Test-Reports') {

      junit 'gameoflife-web/target/surefire-reports/*.xml'
  }

}


