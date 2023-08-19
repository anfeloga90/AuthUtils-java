pipeline {
  agent any

  stages {

    //Dynamic Application Security Testing (DAST)
    //http://myjenkins:8080/sonarqube-webhook 
    //http://mysonarqube:9000
    stage('SonarQube - Static Application Security Testing (SAST)') { //plugin Sonar Quality GatesVersion
      steps {
        sh 'ls -lh'
        withSonarQubeEnv('SonarQube') {
          sh "mvn sonar:sonar \
          -Dsonar-projectKey=Controlador \
          -Dsonar.projectName=Controlador \
          -Dsonar.projectVersion=1.0 \
          -Dsonar.language=Java \
          -Dsonar.sourceEncoding=UTF-8 \
          -Dsonar.host.url=http://mysonarqube:9000 "
        }
      // timeout(time: 2, unit: 'MINUTES') {
      //     script {
      //       waitForQualityGate abortPipeline: true
      //     }
      //   }
      }
    }

    stage('SonarQube - Quality Gate') { //plugin Sonar Quality GatesVersion
      steps {
        timeout(time: 3, unit: 'MINUTES') {
            script {
              waitForQualityGate abortPipeline: true
            }
          }
      }
    }

  }
} 