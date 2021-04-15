pipeline{
        agent any
        stages{
            stage('install docker and docker-compose'){
                steps{
                    sh '''sudo apt-get update
		                  sudo apt install curl -y
                          curl https://get.docker.com | sudo bash
		                  sudo usermod -aG docker $(whoami)
			              sudo apt update
			              sudo apt install -y curl jq
			              version=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r '.tag_name')
		        sudo curl -L "https://github.com/docker/compose/releases/download/${version}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
		        sudo chmod +x /usr/local/bin/docker-compose'''
                }
            }
            stage('deploy'){
                steps{
                    sh 'sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d'
                }
            }
        }
}
