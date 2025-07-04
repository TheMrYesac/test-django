pipeline{
  agent any
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/TheMrYesac/test-django'
      }
    }
    stage('Log In to ECR'){
      steps{
        withAWS(region: 'us-east-2', credentials: 'aws') {
          powershell '''
          $password = aws ecr get-login-password --region us-east-2
          docker login ---username AWS ---password $password 520320208152.dkr.ecr.us-east-2.amazonaws.com
          '''
        }
      }
    }
    stage('Build Docker Image'){
      steps{
        powershell '''
        docker build -t test-django:django .
        docker tag test-django 520320208152.dkr.ecr.us-east-2.amazonaws.com/test-django:django
        '''
      }
    }
    stage('Push Image to ECR'){
      steps{
        powershell '''
        docker push 520320208152.dkr.ecr.us-east-2.amazonaws.com/test-django:django
        '''
      }
    }
  }
}
