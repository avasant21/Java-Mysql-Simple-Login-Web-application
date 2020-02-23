pipeline {
 	agent any
	tools {
		maven 'Maven3.6.3'
		jdk 'Java8'
	}
	stages {
		stage('build_source') {
			steps {
			    sh "ls -ltr"
				sh "mvn clean install package"
   	        }
		}
		stage('docker_image') {
			steps {
			    sh "docker build -t mtwebapp:3.0 ."
   	        }
		}
		stage('docker_push') {
			steps {
			    sh "sudo docker tag mtwebapp:3.0 milindtech/mtwebapp:3.0"
				sh "sudo docker push milindtech/mtwebapp:3.0"
   	        }
		}
		}
		stage('infra_setup') {
			steps {				
			    sh "ansible-playbook -i hosts ec2_setup.yml"
   	        }
		}
		stage('docker_setup') {
			steps {				
			    sh "ansible-playbook -i hosts docker.yml"
   	        }
		}
		stage('container_up') {
			steps {				
			    sh "ansible-playbook -i hosts docker_webapp.yml"
   	        }
		}
	}
}
