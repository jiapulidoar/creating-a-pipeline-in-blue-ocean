pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        curfew()
        sh 'npm install'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          environment {
            Cl = 'true'
          }
          steps {
            sh './jenkins/scripts/test.sh'
            input 'input'
          }
        }

        stage('Test 0 ') {
          steps {
            sh 'echo "Test 0"'
          }
        }

        stage('Test 1') {
          steps {
            sh '''echo "Test 1"
# ./jenkins/scripts/test.sh.'''
          }
        }

        stage('Test 2') {
          steps {
            sh '''echo "Test2"
# ./jenkins/scripts/test.sh.'''
          }
        }

      }
    }

    stage('Deliver') {
      steps {
        curfew()
        sh './jenkins/scripts/deliver.sh'
        input ' Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
}
