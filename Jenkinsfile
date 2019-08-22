node {
  stage('SCM') {
    git 'https://github.com/Sebrag/devops.git'
  }
  stage('SonarQube analysis') {
    def scannerHome = tool 'bugscout';
    withSonarQubeEnv('bs4') {
      // sh "${scannerHome}/bin/sonar-scanner"
      sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=https://bugscout.local -Dsonar.projectName=pip-jenkins -Dsonar.projectVersion=1.0 -Dsonar.projectKey=pip-jenkins -Dsonar.sources=. -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/pip-jenkinsfile -Dsonar.login=xxx -Dsonar.password=xxx"
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
