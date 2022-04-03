def builderImage
def productionImage
def GIT_COMMIT_HASH

pipeline {
    agent any
    stages {
        stage('Checkout Source Code and Logging Into Registry') {
            steps {
                echo 'Logging Into the Private ECR Registry'
                script {
                    GIT_COMMIT_HASH = sh (script: "git log -n 1 --pretty=format:'%H'", returnStdout: true)
                   
                }
            }
        }

        stage('Make A Builder Image') {
            steps {
                echo 'Starting to build the project builder docker image'
                script {
                    builderImage = docker.build("webtest/example-webapp-builder:${GIT_COMMIT_HASH}", "-f ./Dockerfile.builder .")
                  /* builderImage.push()
                    builderImage.push("${env.GIT_BRANCH}")
                    builderImage.inside('-v $WORKSPACE:/output -u root') {
                        sh """
                           cd /output
                           lein uberjar
                        """ 
                    }*/
                }
            }
        }

       /*  stage('Unit Tests') {
             steps {
                  echo 'running unit tests in the builder image.'
                  script {
                      builderImage.inside('-v $WORKSPACE:/output -u root') {
                      sh """
                         cd /output
                         lein test
                      """
                      }
                  }
              }
         }

//         stage('Build Production Image') {
//             steps {
//                 echo 'Starting to build docker image'
//                 script {
//                     productionImage = docker.build("${ACCOUNT_REGISTRY_PREFIX}/example-webapp:${GIT_COMMIT_HASH}")
//                     productionImage.push()
//                     productionImage.push("${env.GIT_BRANCH}")
//                 }
//             }
//         }

 
//         stage('Deploy to Production fixed server') {
//             when {
//                 branch 'release'
//             }
//             steps {
//                 echo 'Deploying release to production'
//                 script {
//                     productionImage.push("deploy")
                   
//                 }
//             }
//         }


//         stage('Integration Tests') {
//             when {
//                 branch 'master'
//             }
//             steps {
//                 echo 'Deploy to test environment and run integration tests'
//                 script {
//                     TEST_ALB_LISTENER_ARN="192.168.248.135:listener/app/testing-website/3a4d20158ad2c734/49cb56d533c1772b"
//                     sh """
//                     ./run-stack.sh example-webapp-test ${TEST_ALB_LISTENER_ARN}
//                     """
//                 }
//                 echo 'Running tests on the integration test environment'
//                 script {
//                     sh """
//                        curl -v http://192.168.248.135:3000 | grep '<title>Welcome to example-webapp</title>'
//                        if [ \$? -eq 0 ]
//                        then
//                            echo tests pass
//                        else
//                            echo tests failed
//                            exit 1
//                        fi
//                     """
//                 }
//             }
//         }

 
//         stage('Deploy to Production') {
//             when {
//                 branch 'master'
//             }
//             steps {
//                 script {
//                     PRODUCTION_ALB_LISTENER_ARN="192.168.248.135/app/production-website/a0459c11ab5707ca/5d21528a13519da6"
//                     sh """
//                     ./run-stack.sh example-webapp-production ${PRODUCTION_ALB_LISTENER_ARN}
//                     """
//                 }
//             }
//         }
    }
}
