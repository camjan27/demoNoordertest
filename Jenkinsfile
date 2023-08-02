  env.DOCKERHUB_USERNAME = 'corine27'

  node() {
    checkout scm

    stage("Unit Test") {
//       sh "docker run --rm -v ${WORKSPACE}:/go/src/cd-demo golang go test cd-demo -v --run Unit"
    }
    stage("Integration Test") {
//       try {
// //         sh "docker build -t cd-demo ."
// //         sh "docker rm -f cd-demo || true"
// //         sh "docker run -d -p 8080:8080 --name=cd-demo cd-demo"
// //         // env variable is used to set the server where go test will connect to run the test
//       }
//       catch(e) {
//         error "Integration Test failed"
//       }finally {
//         sh "docker rm -f cd-demo || true"
//         sh "docker ps -aq | xargs docker rm || true"
//         sh "docker images -aq -f dangling=true | xargs docker rmi || true"
//       }
    }
    stage("Build") {
      sh "docker build -t ${DOCKERHUB_USERNAME}/nt-d:${BUILD_NUMBER} ."
    }
    stage("Publish") {
      withDockerRegistry([credentialsId: 'dockerhub']) {
        sh "docker push ${DOCKERHUB_USERNAME}/NT-d:${BUILD_NUMBER}"
      }
    }
  }
