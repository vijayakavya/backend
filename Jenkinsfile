pipeline {
  agent { label 'workstation'}

  stages {

    stage('Download Dependencies'){
      steps {
        sh 'npm install'
        sh 'env'
      }
    }

    stage('Code Quality'){
   when {
          allof {

           expression { env.TAG_NAME != env.GIT_BRANCH }
          }
        }

          steps {
            sh 'sonar-scanner -Dsonar.host.url=http://18.206.196.93:9000 -Dsonar.login=admin -Dsonar.password=admin123 -Dsonar.projectKey=backend -Dsonar.qualitygate.wait=true'
            echo 'OK'
          }

        }

     stage('Unit Tests'){
     when {
            allof {
               expression { env.TAG_NAME != env.GIT_BRANCH }
               branch 'main'
            }
         }
              steps {
                echo 'CI'
              }
            }


    stage('Release'){
    when {
             expression { env.TAG_NAME ==~ ".*" }
    }
          steps {
             echo 'CI'
          }
        }

  }

}
///