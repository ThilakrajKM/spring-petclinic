pipeline {
	agent any
  
    tools {
		maven 'MAVEN_HOME'
		jdk 'JAVA_HOME'
	}
  
	stages {
		stage('Clean Workspace') {
		  steps {
			sh 'git clean -fdx'
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
          githubNotify gitApiUrl: 'https://github.com/api/v3', context: 'something test', description: 'This commit looks good',  status: 'SUCCESS'
        }
        failure {
          githubNotify gitApiUrl: 'https://github.com/api/v3', context: 'something test', description: 'This commit cannot be built',  status: 'FAILURE'
        }
	}
}
