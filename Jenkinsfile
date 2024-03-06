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
             sh '''sonar-scanner \
            -Dsonar.projectKey=sonar \
            -Dsonar.sources=. \
            -Dsonar.host.url=http://localhost:9000 \
            -Dsonar.token=sqp_ce99c8170361f5bc4ec88a1ebc799f05c1e859a8 '''
          }
        }    
      }
    }
}
