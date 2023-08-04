  env.DOCKERHUB_USERNAME = 'corine27'

  node() {

    stage ("Checkout") {
        checkout scm
    }

    parallel (
        stage("Verschillende checks") {
            'lint':{
                stage("Lint") {
                    sh "echo Run hier je linter"
                }
            },
            'Unit test': {
                stage("Unit Test") {
                    sh "echo Run hier je unit tests"
                }
            },
            'Static security check': {
                stage("Security check") {
                    sh "echo Run hier de security scan"
                }
            }
        }
    )

    stage("Build") {
      sh "docker build -t ${DOCKERHUB_USERNAME}/nt-demo:${BUILD_NUMBER} ."
    }

    stage("Publish") {
      withDockerRegistry([credentialsId: 'dockerhub']) {
        sh "docker push ${DOCKERHUB_USERNAME}/nt-demo:${BUILD_NUMBER}"
      }
    }

    stage("Deploy") {
        sh "echo Run hier je deploy script"
    }

    stage("Regressie test") {
        sh "echo Maak hier je code voor de regressie test"
    }

    stage("Reports") {
        sh "echo Verzamel hier reports en kijk of alles voldoet aan de vooropgestelde criteria"
    }
  }
