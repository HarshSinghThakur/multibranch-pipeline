pipeline {
	agent {
		label {
			label 'built-in'
			customWorkspace '/mnt'
			}
		}
	stages {
		stage ('install-deploy'){
			steps {
				sh "yum install docker -y"
				sh "systemctl start docker" 
				}
			}
		stage ('run') {
			steps {
				sh "docker stop server1 server2 server3"
				sh " docker rm server1 server2 server3"
				sh "docker run --name server1 -itdp 80:80 httpd"
				sh "docker run --name server2 -itdp 90:80 httpd"
				sh "docker run --name server3 -itdp 8085:80 httpd"
				sh "docker cp /mnt/master/multibranch-pipeline/index.html server1:/usr/local/apache2/htdocs"
				sh "docker cp /mnt/22Q1/multibranch-pipeline/index.html server2:/usr/local/apache2/htdocs"
				sh "docker cp /mnt/22Q2/multibranch-pipeline/index.html server3:/usr/local/apache2/htdocs"
				}
			}
		}
}
