pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'python'
        }
      }
      steps {
        sh 'pip install -r requirements.txt'
        sh 'python app.py'
        stash(name: 'compiled-results', includes: '*.py*')
      }
    }
    stage('test') {
      steps {
        sh 'python test.py'
      }
      post {
        always {
          junit 'test-reports/*.xml'
        }
      }    
    }
  }
}