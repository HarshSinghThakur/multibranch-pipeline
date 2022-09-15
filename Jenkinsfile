pipeline {
agent {
label {
label 'built-in'
customWorkspace '/mnt/docker'
}
}
stages {
stage {
steps {
yum install docker -y
systemctl start docker
docker run -itdp 80:80 httpd
id1=$(docker ps -a | awk '{print $1}' | sed -n 2p)
docker cp /mnt/docker/index.html $id1:htdocs
}
}
}
}
