  env.DOCKERHUB_USERNAME = 'corine27'

  node() {
    try {
        stage ("Checkout") {
            checkout scm
        }

        stage("Verschillende checks") {
            parallel (
                'Lint':{
                    stage("Lint") {
                        echo 'Run hier je linter'
                    }
                },
                'Unit test': {
                    stage("Unit Test") {
                        echo 'Run hier je unit tests'
                    }
                },
                'Static security check': {
                    stage("Security check") {
                        echo 'Run hier de security scan'
                    }
                }
            )
        }

        stage("Build") {
          sh "docker build -t ${DOCKERHUB_USERNAME}/nt-demo:${BUILD_NUMBER} ."
        }

        stage("Publish") {
          withDockerRegistry([credentialsId: 'dockerhub']) {
            sh "docker push ${DOCKERHUB_USERNAME}/nt-demo:${BUILD_NUMBER}"
          }
        }

        stage("Deploy") {
            echo 'Run hier je deploy script'
        }

        stage("Regressie test") {
            echo 'Maak hier je code voor de regressie test'
            currentBuild.result = 'FAILURE'
            currentStage.result = 'FAILURE'
        }

        stage("Reports") {
            echo 'Verzamel hier reports en kijk of alles voldoet aan de vooropgestelde criteria'
        }

    } catch (err) {
        currentBuild.result = 'FAILURE'
        println(err.toString())
        println(err.getMessage())
    }

    post {
        success {
            // Custom notification or post-build actions on success
            echo 'Build and deployment successful!'
        }
        failure {
            // Custom notification or post-build actions on failure
            echo 'Build or deployment failed!'
        }
        always {
            echo 'Run hier je cleanup code'
        }
    }
  }
