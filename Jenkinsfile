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
        
	    // CONTAINER IMAGE TESTING
        stage('Container Image Test') {
            steps {
                script {
                    echo 'Running Snyk Container tests'
                    //snykSecurity(snykTokenId: 'Snyk-Token-Plugin', snykInstallation: 'Snyk-Latest', failOnIssues: false, monitorProjectOnBuild: false, severity: 'high', additionalArguments: "--docker --file=${env.WORKSPACE}/Dockerfile $IMAGE_NAME:${env.BUILD_ID}")
		    snykSecurity(snykTokenId: 'snyk_token', snykInstallation: 'Snyk Test', failOnIssues: false)

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
