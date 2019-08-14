node {
  
  stage('SonarQube analysis') {
    def scannerHome = tool 'bugscout';
    withSonarQubeEnv('bs4') {
      // sh "${scannerHome}/bin/sonar-scanner"
      sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=https://bugscout.local -Dsonar.projectName=pip-jenkins -Dsonar.projectVersion=1.0 -Dsonar.projectKey=pip-jenkins -Dsonar.sources=. -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/pip-jenkinsfile -Dsonar.login=gzanella -Dsonar.password=guilherme123"
        }
    }
  stage("Quality Gate") { 
    timeout(time: 5, unit: 'MINUTES') { 
      def qualityGate = waitForQualityGate() 
        if (qualityGate.status != 'OK' && qualityGate.status != 'WARN') {
          error "O código não está de acordo com as regras do BugScout: ${qualityGate.status}"
        } else {
           println "O código está de acordo com as regras do BugScout: ${qualityGate.status}"
        }
    }
  }
}
