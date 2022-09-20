pipeline {
	agent {
	label {
		label 'built-in'
		customWorkspace '/mnt/game-war/'
	}
	}
	stages {
		stage ('Clone-repo') {
		steps {
			sh " rm -rf *"
			sh "git clone https://github.com/Sharsh125/game-of-life.git"
		}
		}
		stage ('build-war') {
		steps {
			dir ('/mnt/game-war/game-of-life/') {
			sh "mvn install -Dmaven.test.skip=true"
			}
		}
		}
		/*
		stage ('Parallel'){
		parallel {
			stage ('deploy-slave1') {
				steps {
					sh "scp -i OhioKey.pem game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.15.245:/mnt/server/apache-tomcat-9.0.65/webapps"
			}
			}
			stage ('deploy-slave2') {
				steps {
					sh "scp -i OhioKey.pem game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.5.111:/mnt/server/apache-tomcat-9.0.65/webapps"
				}
			}
		}
		} 
		*/
}
}
