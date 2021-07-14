pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running Build Automation'
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
