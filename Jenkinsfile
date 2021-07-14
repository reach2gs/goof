pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running Build Automation'
                  }
        }
        stage('Snyk VA scan') {
      tools {
        snyk 'Snyk Test'
      }	
      steps {
        snykSecurity(
          organisation: 'reach2gs',
          severity: 'high',
          snykInstallation: 'Snyk Test',
          snykTokenId: 'snyk_token',
          failOnIssues: 'false'
        )		
      }
    }
		stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("reach2gaurav/snyk-test")
                        }
            }
        }
        
        stage('DeployToProduction') {
            when {
                branch 'master'
            }
            steps {
                input 'Deploy to Production?'
                milestone(1)
                  }
        }
    }
}
