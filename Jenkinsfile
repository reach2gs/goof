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
			  failOnIssues: false, 
			  monitorProjectOnBuild: false, 
                          organisation: 'secpartners-training', 
			  projectName: 'gaurav_appsec_training', 
			  severity: 'critical', 
			  snykInstallation: 'Snyk Test', 
			  snykTokenId: 'Snyk-Token-secpartners-training'
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
        //stage('Container Image Test') {
          //  steps {
            //    script {
                    echo 'Running Snyk Container tests'
                    snykSecurity(snykTokenId: 'snyk_token', snykInstallation: 'Snyk Test', failOnIssues: false, monitorProjectOnBuild: false)

		//}
            //}
        //}
	    
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
