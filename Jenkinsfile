pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-flask-app .'
        sh 'docker tag my-flask-app pgalav/sample'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run my-flask-app python -m pytest app/tests/'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'b3a06214-a0d1-4378-98a7-4adb030379f5', passwordVariable: 'USER_PWD', usernameVariable: 'USER_NM')]) {
          sh "docker login -u ${USER_NM} -p ${USER_PWD}"
          sh 'docker push pgalav/sample'
        }
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
   
