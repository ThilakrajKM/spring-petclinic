pipeline {
	agent any
       
        tools {
		maven 'MAVEN_HOME'
		jdk 'JAVA_HOME'
	}
  
	stages {
		stage('Clean Workspace') {
                          steps {
                                //sh 'git clean -fdx'
                                  script{
                                       def scmVars = checkout scm
                                       env.GIT_COMMIT = scmVars.GIT_COMMIT
                                       env.GIT_BRANCH = scmVars.GIT_BRANCH
                                       echo "${scmVars}"
                                       echo "********************************"
                                       echo "${env}"
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
                success {
                        script {
                                def ref = env.GIT_COMMIT
                                def owner = "ThilakrajKM"
                                def repo = "spring-petclinic"
                                def branchName = env.GIT_BRANCH
                                def result = 'success'
                                def deployStatusBody = '{"state": "' + result + '","target_url": "http://localhost:8080/job/Test_Spring/job/${branchName}/${BUILD_NUMBER}"}'
                                def deployStatusURL = "https://api.github.com/repos/${owner}/${repo}/statuses/${ref}"
                                def deployStatusResponse = httpRequest authentication: 'Githubuserpwd', httpMode: 'POST', requestBody: deployStatusBody , responseHandle: 'STRING', url: deployStatusURL, ignoreSslErrors: 'true'
                                if(deployStatusResponse.status != 201) {
                                        error("Deployment Status API Update Failed: " + deployStatusResponse.status)
                                }
                        }
                }
                failure {
                        script {
                                def ref = env.GIT_COMMIT
                                def owner = "ThilakrajKM"
                                def repo = "spring-petclinic"
                                def branchName = env.GIT_BRANCH
                                def result = 'failure'
                                def deployStatusBody = '{"state": "' + result + '","target_url": "http://localhost:8080/job/Test_Spring/job/${branchName}/${BUILD_NUMBER}"}'
                                def deployStatusURL = "https://api.github.com/repos/${owner}/${repo}/statuses/${ref}"
                                def deployStatusResponse = httpRequest authentication: 'Githubuserpwd', httpMode: 'POST', requestBody: deployStatusBody , responseHandle: 'STRING', url: deployStatusURL, ignoreSslErrors: 'true'
                                if(deployStatusResponse.status != 201) {
                                        error("Deployment Status API Update Failed: " + deployStatusResponse.status)
                                }
                        }
                }
	}
}
