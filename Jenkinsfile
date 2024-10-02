pipeline {
	agent {
		node {
			label "linux && java11"
		}
	}
	environment {
		AUTHOR = "Vini Jumatul Fitri"
		EMAIL = "vinijumatul@gmail.com"
		WEB = "https://vinijumatulf.my.id/"
	}
	// triggers {
	// 	cron("*/5 * * * *")
	// }
	
	stages {
		stage('Prepare') {
			environment {
				APP = credentials("vini_rahasia")
			}
			steps {
				echo("Author ${AUTHOR}")
				echo("Email ${EMAIL}")
				echo("Web ${WEB}")
				echo("Start Job : ${env.JOB_NAME}")
				echo("Start Build : ${env.BUILD_NUMBER}")
				echo("Branch Name : ${env.BRANCH_NAME}")
				echo("App User:  ${APP_USR}")
				echo("App User:  ${APP_PSW}")
				sh("echo 'App Password: ${APP_PSW}' > 'rahasia.txt'")
			}
		}
		
		stage('Build') {
			steps {
				script {
					for (int i = 0; i < 10; i++){
						echo ("Script ${i}")
					}
				}
				echo "Start Build"
				sh("./mvnw clean compile test-compile")
				echo "Finish Build"
			}
		}
		
		stage('Test') {
			steps {
				script {
					def data = [
						"firstName" : "Vini Jumatul",
						"lastName" : "Fitri"
					]
					writeJSON(file: "data.json", json:data)
				}
				echo "Start Test"
				sh("./mvnw test")
				echo "Finish Test"
			}
		}
		
		stage('Deploy') {
			input {
				message "Can we deploy?"
				ok "Yes, of course"
				submitter "admin1, vinijf"
			}
			steps {
				echo "Hello Deploy 1"
				sleep(5)
				echo "Hello Deploy 2"
				echo "Hello Deploy 3"
			}
		}
	}
	post {
		always {
			echo "I will always say hello again!"
		}
		success {
			echo "Yay, Success"
		}
		failure {
			echo "Oh no, failure!"
		}
		cleanup {
			echo "Don't care success or error"
		}
	}
}

