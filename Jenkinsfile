pipeline {
  agent any
  stages{
    stage('Build'){
      steps{
        sh 'mvn clean package'
      }
      post{
        success{
          echo 'Now Archiving....'
          archiveArtifacts artifacts: '**/target/*.war'
        
        }
      }
    }
    stage ('Deploy to Staging '){
      steps{
        build job: 'Deploy-to-staging'
      }
    }
    stage ('Deploy to prodution'){
      steps{
        timeout(time:5, unit:'DAYS'){
          input message: 'Approve PRODUCTION Deployement?'
        }
        build job: 'Deploy-to-prod'
      }
      post{
        success{
          echo 'Code deployed to Production.'
        }
        failure{
          echo 'Deployement failed'
        }
      }
    }
  }
}
