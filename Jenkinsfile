//pipeline {
//    agent any
//    stages {
 //       stage('Build') {
 //           steps {
                // Get some code from a GitHub repository
 //               git url: 'https://github.com/songjz1997/simple-python-pyinstaller-app.git', branch: 'master'
 //               sh "python3 -m py_compile sources/add2vals.py sources/calc.py"
//            }
//        }
//        stage('Test') {
//            steps {
                //sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
//                sh 'python3 sources/test_calc.py'
//            }
//        }
//        stage('Deliver') {
//            steps {
//                sh 'echo "The python application delivered!"'
                //sh 'pyinstaller --onefile sources/add2vals.py'
//            }
            //post {
               // success {
                    //archiveArtifacts 'dist/add2vals'
         //       }
         //   }
//        }
//    }
//}

pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') { 
            agent {
                docker {
                    image 'qnib/pytest' 
                }
            }
            steps {
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py' 
            }
            post {
                always {
                    junit 'test-reports/results.xml' 
                }
            }
        }
    }
}

