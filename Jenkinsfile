pipeline {
   stages { 
  agent { label 'HRMS&&QA' }
  triggers { cron('50 * * * 1-2') }
  parameters {
      string(
             name: 'JunitReportsPath', 
             defaultValue: 'gameoflife-web/target/surefire-reports/*.xml', 
             description: 'Location for the Junit Reports'
      ) 

      string(
              name: 'Artifacts',
              defaultValue: 'gameoflife-web/target/*.war',
              description: 'Path for the Artifacts'
            )

      choice(
              name: 'Branch',
              choices: ['scripted', 'declarative', 'master'],
              description: 'Pick which ever branch you like'
            )        
      
   }
} 
} 
  

  stages {
      stage ('git') {

          steps {
              git branch: "${params.Branch}", url: 'https://github.com/mitchelwize77/game-of-life'
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
     stage ('postbuild') {

         steps {
             junit testResults: "${params.JunitReportsPath}"
             
             archive includes: "${params.Artifacts}"

        }

     }  

  }

    