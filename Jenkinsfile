pipeline {
	agent {
		label {
			label 's2'
	}
	}
	stages {
		stage ('cloning') {
			steps {
			dir ('/mnt/22Q2/') {
			sh "rm -rf /mnt/22Q2/multibranch-pipeline"
			sh "git clone https://github.com/Sharsh125/multibranch-pipeline.git -b 22Q2"
			sh "sudo chmod -R 777 /mnt/22Q2"
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
			sh "sudo cp /mnt/22Q2/multibranch-pipeline/index.html /var/www/html/"
				}
		}
	}
}
