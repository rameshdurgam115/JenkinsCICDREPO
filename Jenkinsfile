pipeline {
  agent any
  environment {
    IMAGE_NAME = "fastapi-jenkins"
    CONTAINER_NAME = "fastapi_app"
    APP_PORT = "8000"
  }
  stages {
    stage('Checkout') {
      steps {
        // Replace with your GitHub repo URL and Jenkins credential ID
        git url: 'https://github.com/rameshdurgam115/JenkinsCICDREPO.git', credentialsId: 'github-pat'
      }
    }
    stage('Build Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME .'
      }
    }
    stage('Replace Container') {
      steps {
        sh '''
          docker stop $CONTAINER_NAME || true
          docker rm   $CONTAINER_NAME || true
          docker run -d --name $CONTAINER_NAME -p $APP_PORT:$APP_PORT $IMAGE_NAME
        '''
      }
    }
  }
  post {
    success { echo "Deployment succeeded; app is live on port $APP_PORT" }
    failure { echo "Deployment failed; check the logs" }
  }
}
