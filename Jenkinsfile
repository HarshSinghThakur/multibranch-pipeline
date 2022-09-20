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
			sh "rm -rf *"
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
		stage ('deploy-slave') {
				steps {
					sh "cp /mnt/OhioKey.pem /mnt/game-war"
					sh "scp -i OhioKey.pem /mnt/game-war/game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.11.176:/mnt"
					sh "scp -i OhioKey.pem /mnt/Dockerfile ec2-user@172.31.11.176:/mnt"
					sh "scp -i OhioKey.pem /mnt/game-war/game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.11.4:/mnt"
					sh "scp -i OhioKey.pem /mnt/Dockerfile ec2-user@172.31.11.4:/mnt"
				}
		}				
		stage ('parallel-stages') {
		parallel {
			stage ('slave1-container') {
				agent {
				node {	
				label 'slave1'
				customWorkspace "/mnt/"
				}		
				}
				steps {
				sh "sudo yum install docker -y"
				sh "systemctl start docker"
				sh "docker build -t myserver:1.0 ."
				sh "docker run -dp 8081:8080 myserver:1.0"
				}
				}
				stage ('slave2-container') {
				agent {
				node {	
				label 'slave2'
				customWorkspace "/mnt/"
				}		
				}
				steps {
				sh "sudo yum install docker -y"
				sh "systemctl start docker"
				sh "docker build -t myserver:2.0 ."
				sh "docker run -dp 8081:8080 myserver:2.0"
				}
				}
		
		}
		}
}
}
