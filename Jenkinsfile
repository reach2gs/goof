pipeline {
  agent any
  stages {
    stage('Snyk VA scan') {
      tools {
        snyk 'Snyk Test'
      }	
      steps {
        snykSecurity(
          organisation: 'reach2gs',
          severity: 'high',
          snykInstallation: 'Snyk Test',
          snykTokenId: 'snyk token',
          targetFile: 'requirements.txt',
          failOnIssues: 'true'
        )		
      }
    }
  }
}
