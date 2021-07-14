pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running Build Automation'
                  }
        }
         stage('Snyk SCA scan') {
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
        
	    // CONTAINER IMAGE TESTING
        stage('Container Image Test') {
            steps {
                script {
                    echo 'Running Snyk Container tests'
                    snykSecurity(snykTokenId: 'snyk_token', snykInstallation: 'Snyk Test', failOnIssues: false, monitorProjectOnBuild: true)

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
