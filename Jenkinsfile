@Library("belajar-jenkins-shared-library@main")_

import programmerzamannow.jenkins.Output;

pipeline {
	agent any
	stages {
		stage("Global Variable") {
			steps {
				script {
					echo(author())
					echo(author.name())
					echo(author.channel())
				}
			}
		}
		stage("Hello Groovy") {
			steps {
				script {
					Output.hello(this, "Groovy")
				}
			}
		}
	}
}
