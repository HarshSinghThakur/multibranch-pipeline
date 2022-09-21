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
			stage ('slave1-cont') {
				agent {
				label {
				label 'slave1'
				customWorkspace '/mnt/slave1'
				}
				}
				steps {
				sh "sudo yum install docker -y"
				sh "sudo systemctl start docker"
				sh "sudo cp /mnt/Dockerfile /mnt/slave1/"
				sh "sudo cp /mnt/gameoflife.war /mnt/slave1/"
				sh "sudo docker build -t tomcat:1.0 ."
				sh "sudo docker run --name tm-server1 -dp 8081:8080 -v /mnt/myserver-logs:/usr/local/tomcat/logs tomcat:1.0"
				}
				}
				stage ('slave2-cont') {
				agent {
				label {
				label 'slave2'
				customWorkspace '/mnt/slave2'
				}
				}
				steps {
				sh "sudo yum install docker -y"
				sh "sudo systemctl start docker"
				sh "sudo cp /mnt/Dockerfile /mnt/slave2/"
				sh "sudo cp /mnt/gameoflife.war /mnt/slave2/"
				sh "sudo docker build -t tomcat:2.0 ."
				sh "sudo docker run --name tm-server2 -dp 8082:8080 -v /mnt/myserver-logs:/usr/local/tomcat/logs tomcat:2.0"
				}
				}
		
		}
		}
}
}
