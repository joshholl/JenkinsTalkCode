pipeline {
	agent {
        	docker { image 'node:current-alpine' }
    } 
	stages {
		stage('build') {
			steps {
				dir('fizzbuzz') {
					sh "npm ci"
					sh "npm run build"
				}
			}
	
		}
		stage('test') {
			steps {
				dir('fizzbuzz') {
				}
			}
		}
		stage('deploy') { 
			input {
				message "Should we really deploy"
				ok "Sure thing boss"
			}
			steps {
				withAWS(credentials: 'MyAwsCredentials') {
					s3Upload(
						bucket: "jenkins-tech-talk",
						file: "fizzbuzz/build"

					)
				}
			}
		}
	}
	post {
		always {
			echo "All Done!!!"
		}
	}
}
