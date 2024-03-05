pipeline{
  agent any
  stages{
    stage("Checkout"){
      steps{
        git credentialsId: "git-threepoints-github", url:"git@github.com/lucaza21/threepoints_devops_webserver.git"
      }
    }
    stage("Pruebas SAST"){
      steps{
        echo "Ejecucion de pruebas SAST"
      }
    }
    stage("Build"){
      steps{
        sh "docker build -t devops_ws"
      }
    }
    
