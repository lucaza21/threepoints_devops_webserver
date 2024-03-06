pipeline{
  agent any
  stages{
    stage("Checkout"){
      steps{
        git credentialsId: 'github_user_threepoints', url: 'https://github.com/lucaza21/threepoints_devops_webserver'
      }
    }
    stage("Pruebas SAST"){
      steps{
        echo "Ejecucion de pruebas SAST"
      }
    }
    stage("Build"){
      steps{
        script{
          sh "docker build -t devops_ws ."
        }
      }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'Sonarqube';
      }
      steps{
        withSonarQubeEnv(credentialsId: 'jenkins-1') {
            sonar.projectKey=practica_1_jenkins
            sonar.projectName=practica_1_jenkins
            sonar.projectVersion=1.0
            sonar.language=java
            sonar.tests=src/test/java
            sonar.sources=src/main/java
          }
        }    
      }
    }
}
