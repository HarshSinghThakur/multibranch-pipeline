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
			sh "rm -rf /mnt/22Q1/multibranch-pipeline"
			sh "git clone https://github.com/Sharsh125/multibranch-pipeline.git -b 22Q1"
			sh "sudo chmod -R 777 /mnt"
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
			sh "sudo cp /mnt/22Q1/multibranch-pipeline/index.html /var/www/html/"
				}
			}
	}
}
