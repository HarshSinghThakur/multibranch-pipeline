pipeline {
agent {
label {
label 'built-in'
customWorkspace '/mnt/docker'
}
}
stages {
stage ('install-deply'){
steps {
sh "yum install docker -y"
sh "systemctl start docker"
sh "docker run -itdp 80:80 httpd"
}
stage ('copy') {
steps {
script { 
id=${(docker ps -a | awk '{print $1}' | sed -n 2p)}
}
}
}
}
}
}
