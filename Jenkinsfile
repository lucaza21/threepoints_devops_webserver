pipeline{
  agent any
  stages{
    stage("Checkout"){
      steps{
        git credentialsId: "github_user_threepoints", url:"git@github.com/lucaza21/threepoints_devops_webserver.git"
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
  }
}
