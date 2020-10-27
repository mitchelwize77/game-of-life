node('HRMS&&QA') {
  def responses = null
    stage('selection'){
        responses = input message: 'Enter branch and select build type',
        parameters: [string(defaultValue: '', description: 'Enter the branch', name: 'BRANCH_NAME'),
                     choice(choices: 'DEBUG\nRELEASE', description: 'BUILD Type', name: 'BUILD_TYPE')]

    }

    stage('git') {
        git 'https://github.com/mitchelwize77/game-of-life.git'
    }
    stage('build') {
        sh 'mvn clean package'
        if (responses.BUILD_TYPE == 'DEBUG'){
            sh 'mvn clean package'
        }
        if (responses.BUILD_TYPE == 'RELEASE'){
            sh 'mvn clean install'
        }

    }
    stage('testresults'){
        junit 'gameoflife-web/target/surefire-reports/*.xml'
    }
}    