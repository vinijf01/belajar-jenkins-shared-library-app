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
	parameters {
		string(name: 'NAME', defaultValue: "Guest", description: "What is your name?")
		text(name: 'DESCRIPTION', defaultValue: "Guest", description: "Tell me about you?")
		booleanParam(name: 'DEPLOY', defaultValue: false, description: "Need to deploy?")
		choice(name: 'SOCIAL_MEDIA', choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
		password(name: 'SECRET', defaultValue: "", description: "Encrypt Key")
	}
	//option {
	//	disableConcurrentBuilds()
	//	timeout(time: 10, unit: 'MINUTES')
	//}
	// triggers {
	// 	cron("*/5 * * * *")
	// }
	
	stages {
		stage('OS Setup') {
			matrix {
				axes {
					axis {
						name "OS"
						values "linux", "windows", "mac"
					}
					axis {
						name "ARC"
						values "32", "64"
					}	
				}
				stages {
				stage("OS SETUP"){
					steps {
						echo("Setup ${OS} ${ARC}}")
					}
				}
			}
			}
			
		}
		stage('Preperation'){
			parallel {
				stage('Prepare Java'){
					steps {
						echo("Prepare Java")
					}
				}
				stage('Prepare Maven'){
					steps {
						echo("Prepare Maven")
					}
				}
			}
		}
		stage('Parameter'){
			steps {
				echo "Hello ${params.NAME}!"
				echo "You description is ${params.DESCRIPTION}!"
				echo "You social media is ${params.SOCIAL_MEDIA} user!"
				echo "You to deploy ${params.DEPLOY} to deploy!"
				echo "You secret is ${params.SECRET}!"
			}
		}
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
				//echo("App User:  ${APP_PSW}")
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
				parameters{
					choice(name: 'TARGET_ENV', choices: ['DEV', 'QA', 'PROD'], description: 'We will deploy to?')
				}
			}
			steps {
				echo("Deploy to ${TARGET_ENV}")
			}
		}
		stage ('Release'){
			when {
				expression {
					return params.DEPLOY
				}
			}
			steps {
				echo("Release it")
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

