pipeline{
  agent any
  stages{
    stage("Checkout"){
      steps{
        git credentialsId: 'github_user_threepoints', url: 'https://github.com/lucaza21/threepoints_devops_webserver'
      }
    }
    stage("Pruebas Paralelas"){
      parallel{
        stage("Pruebas SAST"){
          steps{
            echo "Ejecucion de pruebas SAST"
            }  
          }
        stage("Imprimir Env"){
          steps{
            echo "El Workspace es: ${WORKSPACE}"
            }  
          }
      }
    }
    stage("Configurar archivo") {
        steps { withCredentials([usernamePassword(credentialsId: 'Credentials_Threepoints',
                     usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
            sh ''' 
              echo "[credentials]\n" > credentials.txt
              echo "user=${USER}" >> credentials.txt
              echo "password={PASSWORD}" >> credentials.txt
              
              cat credentials.txt
            '''        
          }
         archiveArtifacts artifacts: 'credentials.txt', onlyIfSuccessful: true
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
            -Dsonar.sources=. \
            -Dsonar.token=sqp_488fe4252038465d68192cf05c9aab83a3aff7ef
            '''
              }
          }
      }
    }
}
