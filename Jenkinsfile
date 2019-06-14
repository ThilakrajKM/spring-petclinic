pipeline {
	agent any
        
        def scmVars
        
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
                                scmVars = checkout scm
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
                        githubNotify gitApiUrl: 'https://github.com/api/v3', context: 'something test', description: 'This commit looks good',  status: 'SUCCESS', 
                                credentialsId: "Githubuserpwd", repo: 'spring-petclinic', account: "ThilakrajKM", sha: scmVars.GIT_COMMIT
                }
                failure {
                        githubNotify gitApiUrl: 'https://github.com/api/v3', context: 'something test', description: 'This commit cannot be built',  status: 'FAILURE',
                                credentialsId: "Githubuserpwd", repo: 'spring-petclinic', account: "ThilakrajKM", sha: scmVars.GIT_COMMIT
                }
	}
}
