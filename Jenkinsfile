pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'python:2-alpine'
        }

<<<<<<< HEAD
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?'
            }
        }

        stage('Deliver') {
            agent {
                docker {
                    image 'cdrx/pyinstaller-linux:python2'
                }
            }
            steps {
                sh 'pyinstaller --onefile sources/add2vals.py'
                
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
=======
      }
      steps {
        sh 'python -m py_compile sources/add2vals.py sources/calc.py'
      }
>>>>>>> 2d60a08f99bc5a7bdc2307f511418d58a9374831
    }

    stage('Test') {
      agent {
        docker {
          image 'qnib/pytest'
        }

      }
      post {
        always {
          junit 'test-reports/results.xml'
        }

      }
      steps {
        sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
      }
    }

    stage('Manual Approval') {
      steps {
        input 'Lanjutkan ke tahap Deploy?'
      }
    }

    stage('Deliver') {
      agent {
        docker {
          image 'cdrx/pyinstaller-linux:python2'
        }

      }
      post {
        success {
          archiveArtifacts 'dist/add2vals'
        }

      }
      steps {
        sh 'pyinstaller --onefile sources/add2vals.py'
        sh 'sleep 60'
      }
    }

  }
}