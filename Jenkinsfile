node {
  try {
   // Mark the code checkout 'stage'....
   stage 'checkout'
   git branch: env.BRANCH_NAME, url: 'https://github.com/ThilakrajKM/spring-petclinic.git'
   
   stage 'get dist from ui'
   sh '''cp -r ~/dist.tar.gz .
   tar -xzvf dist.tar.gz
   rm -rf src/main/resources/static/*
   cp -r dist/* src/main/resources/static/
   chown -R jenkins:jenkins src'''
   
   stage 'build and test'
   sh "mvn clean package "
   
   stage('Cleanup') {
	deleteDir()
   }
 
   notifySuccessful()
  } catch (e) {
    currentBuild.result = "FAILED"
    notifyFailed()
    throw e
  }
}
def notifySuccessful() {
	emailext (
      subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
      to: 	'thilakraj.mahabala.com',
      cc: 	'thilakraj.mahabala.com', 
      bcc: 	'thilakraj.mahabala@tavant.com',
      recipientProviders: [[$class: 'CulpritsRecipientProvider'],[$class: 'RequesterRecipientProvider'],[$class: 'DevelopersRecipientProvider']]
    )
}
def notifyFailed() {
	emailext (
      subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
      to:  'thilakraj.mahabala@tavant.com',
      cc:  'thilakraj.mahabala@tavant.com', 
      bcc: 'thilakraj.mahabala@tavant.com',
      recipientProviders: [[$class: 'CulpritsRecipientProvider'],[$class: 'RequesterRecipientProvider'],[$class: 'DevelopersRecipientProvider']]
    )
}
