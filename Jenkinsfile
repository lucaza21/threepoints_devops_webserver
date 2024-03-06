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
    stage('SonarCloud') {
      environment {
        SCANNER_HOME = tool 'SonarScanner'
        PROJECT_NAME = "sonar"
      }
      steps {
        withSonarQubeEnv(installationName:'Sonarqube', credentialsId: 'jenkins-1') {
            sh '''$SCANNER_HOME/bin/sonar-scanner \
            -Dsonar.java.binaries=build/classes/java/ \
            -Dsonar.projectKey=$PROJECT_NAME \
            -Dsonar.projectName=$PROJECT_NAME \
            -Dsonar.sources=.
            -Dsonar.host.url=http://localhost:9000 \
            -Dsonar.token=sqp_ce99c8170361f5bc4ec88a1ebc799f05c1e859a8
          '''
              }
          }
      }
    }
}
