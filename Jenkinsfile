pipeline{
	agent {
		label{
			label "built-in"
		}
	}
	parameters{
		string(name: "PORT", description: "Please assign one port number to docker container:")
	}
	stages{
		stage("Cleaning workspace"){
			steps{
				cleanWs ()
			}

		}
		stage("checkout scm"){
			steps{
				checkout scm 
			}

		}
		stage("remmoving if containre is running"){
			steps{
				sh "sudo docker container rm -f httpd_${GIT_BRANCH} || true"
		        }
		}
		stage("Creating docker volume"){
        		steps{
				sh "sudo docker volume create http_volume"
        		}

            }
        stage("Creating container"){
        	steps{
				sh "sudo docker run -dp ${PORT}:80 --name httpd_${GIT_BRANCH} -p http_volume:/usr/local/apache2/htdocs/ httpd"
        	}

         }
            
		stage("Coping index file to container:"){
			steps{
				sh "sudo docker cp $WORKSPACE/index.html /var/lib/docker/volumes/http_volume"
			}
		}
	}
	
}
