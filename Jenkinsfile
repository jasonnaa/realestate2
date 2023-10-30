node('AppServer')
{
  def app
  stage('Cloning Git')
  {
    checkout scm
  }

  stage('Build and Tag')
  {
    app = docker.build("jasonnaa/realestate2")
  }

  stage('Post-to-dockerhub')
  {
    docker.withRegistry('https://registry.hub.docker.com','dockerhub_credentials')
    {
      app.push("latest")
    }
  }
  stage('Pull-image-server')
  {
    sh "docker-compose down"
    sh "docker-compose up -d"
  }
}
