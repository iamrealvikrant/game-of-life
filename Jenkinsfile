pipeline {
	agent {
	label {
	label ('built-in')
	//customWorkspace '/mnt/sample'//
	}
	}
	stages {
		stage ('install docker , maven, git') {
		steps {
			sh 'yum install docker git maven -y ; systemctl start docker '
		}
		}
		stage ('cloning repo') {
		steps {
			sh 'rm -rf /mnt/sample/*'
			sh 'git clone https://github.com/iamrealvikrant/game-of-life.git'
		}
		}
		stage ('build gameoflife') {
		steps {
			sh 'cd /mnt/sample/game-of-life/ ; mvn clean package'
		}
		}
    //comment below stage after first build//
    stage ('installing docker-compose') { 
		steps {
			 sh 'curl -SL https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose ; sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose'
			 sh 'chmod -R 777 /usr/bin/docker-compose ; chmod -R 777 /usr/local/bin/docker-compose'
		}
		}
		stage ('depoly to tomcat container') {
		steps {
			sh 'cd /mnt/sample/game-of-life/ ; sudo docker-compose up tomcat_service -d'
		}
		}
	}
}
