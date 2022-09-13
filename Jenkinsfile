pipeline {
	agent {
		label {
			label 'built-in'
	}
	}
	stages {
		stage ('cloning') {
			steps {
			dir ('/mnt/master/') {
			sh "rm -rf /mnt/master/multibranch-pipeline"
			sh "git clone https://github.com/Sharsh125/multibranch-pipeline.git -b master"
			sh "chmod -R 777 /mnt/master"
			}
			}
		}
		stage ('install httpd ') {
			steps {
			sh "yum install httpd -y"
			sh "service httpd start"
			sh "chkconfig httpd on"
			sh "chmod -R 777 /var/www/html"
				}
			}
			stage ('deploy-index') {
			steps {
			sh " cp /mnt/master/multibranch-pipeline/index.html /var/www/html/index.html"
				}
			}
	}
}
