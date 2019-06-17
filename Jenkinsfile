pipeline {
	agent any
       
        
        /*githubNotify gitApiUrl: 'https://github.com/api/v3', context: 'something test', description: 'This commit looks good',  status: 'PENDING', 
                          credentialsId: "Githubuserpwd", repo: 'spring-petclinic', account: "${GITHUB_PR_SOURCE_REPO_OWNER}", sha: "${GITHUB_PR_HEAD_SHA}"*/
  
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
                        //script {
                                curl -k "https://api.github.com/ThilakrajKM/spring-petclinic/statuses/$env.GIT_COMMIT?access_token=91affb85754203f7b796820a995e1540292bce1e"  -H "Content-Type: application/json" -X POST  -d "{\"state\": \"success\", \"description\": \"Jenkins\", \"target_url\": \"http://10.131.155.89:8080\"}"
                        //}
                }
                failure {
                        //script {
                                curl -k "https://api.github.com/ThilakrajKM/spring-petclinic/statuses/$env.GIT_COMMIT?access_token=91affb85754203f7b796820a995e1540292bce1e"  -H "Content-Type: application/json" -X POST  -d "{\"state\": \"failure\", \"description\": \"Jenkins\", \"target_url\": \"http://10.131.155.89:8080\"}"
                        //}
                }
	}
}
