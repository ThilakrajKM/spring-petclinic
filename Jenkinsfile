#!groovy

pipeline{

    agent{ 
        label "master"
    }
    
    tools{
        maven "MAVEN_HOME"
        jdk "JAVA_HOME"
    }
    
    /*options {
        gitLabConnection('tavant-gitlab')
    }*/
   
    stages{
    
    	stage('Clean Workspace'){
            steps{
                sh "git clean -fdx"
            }
        }
        
        stage('Build'){
            steps{
                 sh  "mvn clean package -DskipTests=true"
            }
        }
        
    }
    post {
		success{
			//sendMail('All Stages Executed SucessFully')
		}
	}  
}
def sendMail(mail_subject ){
	emailext attachLog: false,
		//	body: '${JELLY_SCRIPT,template="jenkins-html-custom"}',
			recipientProviders: [developers()],
			mimeType: 'text/html' ,
			subject: mail_subject,
			body: '''Build Branch : \'${BRANCH_NAME}\' 
				JOB NAME : \'${JOB_NAME}\' 
				BUILD NUMBER :  (${BUILD_NUMBER})  
				BUILD URL :  ${BUILD_URL} 
				''' 
}
