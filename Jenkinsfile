//demo code for pipeline
def devname
def git_id
def stagename
def app
node {
 	
    try {
        stage ('SCM') {
		deleteDir()
		//cleanWs()
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'mygetid', url: 'git@github.com:kailastambe/rahul.git']]])
		stageName="CHECKOUT"
		git_id = sh (returnStdout: true, script:"""git log --oneline --pretty=format:"%H" | head -n 1 """).trim()
				println git_id
				devname = sh (returnStdout: true, script:"""git log --pretty=format:"%ae" | head -1""")

println devname
		                app = sh (returnStdout: true, script: """git log --pretty=format:"%ce" | head -1 """).trim()
		                println app
        }
        stage ('Build') {
		stagename="BUILD"
		def stage="Build"
        	sh "echo 'shell scripts to build project...'"
		succEmail(stage,devname,git_id)
        }
        stage ('Tests') {
		stagename="TEST"
		def stage="Test"
	        parallel 'static': {
	            sh "echo 'shell scripts to run static tests...'"
	        },
'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests.....'"
	        }
		succEmail(stage,devname,git_id)
        }
      	stage ('Deploy') {
		stagename="DEPLOY"
		def stage="Deploy"
            sh "echo 'shell scripts to deploy to server...'"
			succEmail(stage,devname,git_id)
      	}
} catch (err) {
                     echo "Build failed with exception: "
				println(err)
				JobResult = "FAILED"
				currentBuild.result = "FAILED"
				notifyFailed(devname)
	            throw err
    }
}
def succEmail(stage,devname,git_id) {
		
		 emailext (
					subject: "${stage}: Deployment Success | BUILD #${env.BUILD_NUMBER}",
					
					 body: """
              		
              		"""
              		,
              		mimeType: 'text/html',
			attachLog: true,
              		to: devname
			
					)			
		echo "Job success mail"
	}
def notifyFailed(devname) {
  emailext (
      subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]': Check console output at '${env.BUILD_URL}' [${env.BUILD_NUMBER}]",
      to: devname
    )
}
