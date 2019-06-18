pipeline {
  agent any
  stages {
    stage('Clean Workspace') {
      steps {
        script {
          def scmVars = checkout scm
          env.GIT_COMMIT = scmVars.GIT_COMMIT
          env.GIT_BRANCH = scmVars.GIT_BRANCH
          echo "${scmVars}"
          echo "********************************"
          echo "${env}"
          updateGitComitStatus('pending','Build is pending')
          echo "done"
        }

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