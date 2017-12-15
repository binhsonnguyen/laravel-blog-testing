pipeline {
  agent {
    docker { image 'docker:rc' }
  }

  environment {
    QUALITY_CHECK = 'true'
  }

  stages {
    stage('Warmup') {
      steps {
        sh 'printenv'
        sh 'docker -v'
        sh 'pwd'
        sh 'ls'
        sh 'ping -c4 scrumlab.agilead.vn'
      }
    }

    stage('Quality Check') {
      steps {
        sh 'docker run --rm -v $(pwd):/root/src binhsonnguyen/sonarqube-scanner'
        sh 'cat .scannerwork/report-task.txt'
      }
    }
  }

  post {
    always {
      echo 'POST: clean up our workspace'
      deleteDir()
    }
    success {
      echo 'POST: success'
    }
    failure {
      echo 'POST: failed'
    }
    unstable {
      echo 'POST: unstable'
    }
    changed {
      echo 'POST: changed'
    }
  }
}