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
			sh "git clone https://github.com/HarshSinghThakur/game-of-life.git"
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
					sh "scp -i OhioKey.pem /mnt/game-war/game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.11.176:/mnt/slave1"
					sh "scp -i OhioKey.pem /mnt/Dockerfile ec2-user@172.31.11.176:/mnt/slave1"
					sh "scp -i OhioKey.pem /mnt/game-war/game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.11.4:/mnt/slave2"
					sh "scp -i OhioKey.pem /mnt/Dockerfile ec2-user@172.31.11.4:/mnt/slave2"
				}
		}
		stage ('slave-jobs') {
			steps {
			build 'slave-job'
			}
		}
		
}
}
