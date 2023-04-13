pipeline 
{
  agent any

  tools
    {
        maven 'maven-3.9.0'
    }

  stages 
  {
    stage('Build') 
    {
      steps 
      {
        sh 'mvn clean package'
        sh "docker build -t rency1192/practicalexam ."
        
      }
    }
    stage('Test') 
    {
      steps 
      {
        sh 'mvn test'
      }
    }
    stage('Deploy') 
    {
        steps 
        {
                script
                {
                echo 'deploying the application'
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
                {
                    sh "echo ${PASSWORD} | docker login -u ${USERNAME} --password-stdin"
                    sh "docker push rency1192/practicalexam:${IMAGE_NAME}"
                }
                }
        }
    }
  }
}
