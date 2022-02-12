pipeline{
  agent {label 'worker'}
  triggers{
    cron('0 */4 * * *')
  }
  tools {
    maven "maven"
  }
  parameters{
    string(name: 'BRANCH', defaultValue: 'Master')
    choice(name: 'OPERATION', choices: ['A','S','M','D'])
  }
  options {
    timeout(time: 3, unit: 'MINUTES')
    retry(3)
    disableConcurrentBuilds()
  }
  stages{
    stage("input runtime"){
      input{
        message "Do you want to proceed?"
        ok "YES"
      }
      steps{
        echo "testing"
      }
    }
    stage("Parallel stages"){
    parallel{
      stage("Build Stage"){
        steps{
          sh "echo building and pusing the docker image"
          echo "Hello ${params.BRANCH}"
        }
      }
      stage("Testing Stage"){
        steps{
          sh "sleep 1"
        }
      }
    }
    }
  }
  post {
    always{
      echo "RUN ALWAYS"
    }
  }
}
