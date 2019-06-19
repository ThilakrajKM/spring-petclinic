pipeline {
	agent any
       
        tools {
		maven 'MAVEN_HOME'
		jdk 'JAVA_HOME'
	}
  
	stages {
		stage('Checkout') {
                          steps {
                                //sh 'git clean -fdx'
                                  script{
                                       def scmVars = checkout scm
                                       env.GIT_COMMIT = scmVars.GIT_COMMIT
                                       env.GIT_BRANCH = scmVars.GIT_BRANCH
                                       echo "${scmVars}"
                                       echo "********************************"
                                       echo "${env}"
                                       updateGitComitStatus('pending','Build is pending')
                                       echo "Checkout Complete"
                                          
                                  }
                          }
		}
		stage('Build') {
                          steps {
                                sh 'mvn clean package -DskipTests=true'
                          }
		}
		
	}

	post {
                //need to create a function
                success {
                        script {
                                updateGitComitStatus('success','Build has completed successfully')
                        }
                }
                failure {
                        script {
                                updateGitComitStatus('failure','Unable to build the project')
                        }
                }
	}
        
	
}

def updateGitComitStatus(String resultStatus, String resultMessage){

        def ref = env.GIT_COMMIT
        def owner = "ThilakrajKM"
        def repo = "spring-petclinic"
        def branchName = env.GIT_BRANCH
        def result = 'failure'
        def deployStatusBody = '{"state": "' + resultStatus + '", "context":"CI-Jenkins", "description": "' + resultMessage + '" ,   "target_url": "http://localhost:8080/job/Test_Spring/job/${branchName}/${BUILD_NUMBER}"}'
        def deployStatusURL = "https://api.github.com/repos/${owner}/${repo}/statuses/${ref}"
        def deployStatusResponse = httpRequest authentication: 'Githubuserpwd', httpMode: 'POST', requestBody: deployStatusBody , responseHandle: 'STRING', url: deployStatusURL, ignoreSslErrors: 'true'
        if(deployStatusResponse.status != 201) {
                error("Deployment Status API Update Failed: " + deployStatusResponse.status)
        }

}
