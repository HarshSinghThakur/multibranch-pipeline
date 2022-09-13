pipeline {
	agent {
		label {
			label 's1'
	}
	}
	stages {
		stage ('cloning') {
			steps {
			dir ('/mnt/22Q1/') {
			sh "git clone url -b 22Q1"
			sh "sudo chmod -R 777 /mnt/22Q1"
			}
			}
		}
		stage ('install httpd ') {
			steps {
			sh "sudo yum install httpd -y"
			sh "sudo service httpd start"
			sh "sudo chkconfig httpd on"
			sh "sudo chmod -R 777 /var/www/html"
				}
			}
			stage ('deploy-index') {
			steps {
			sh "sudo cp /mnt/22Q1/multibranch/index.html /var/www/html/index.html"
				}
			}
	}
}
