pipeline {

	agent any
	
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
	tools {
		maven 'MAVEN_HOME'
		jdk 'JAVA_HOME'
	}
	post {
		success {
			echo 'Sucess'
		}
	}
}

