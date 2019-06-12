node {

    stage('Checkout') {
        git 'https://github.com/ThilakrajKM/spring-petclinic'
    }
	
	stage('Build') {
	
    }

    stage('Archive') {
    }
    
    stage('Publish Status'){
        githubPRStatusPublisher buildMessage: message(failureMsg: githubPRMessage('Can\'t set status; build failed.'), successMsg: githubPRMessage('Can\'t set status; build succeeded.')), statusMsg: githubPRMessage('${GITHUB_PR_COND_REF} run ended'), unstableAs: 'FAILURE'
    }

}