pipeline{
    agent any 
    stages{
        stage("Building stage"){
            steps{
                sh '''
                ssh -i var/lib/jenkins/docker.pem -t -o StrictHostKeyChecking=no ubuntu@ec2-54-224-221-143.compute-1.amazonaws.com
                sudo apt-get update
                sudo apt-get install \
                ca-certificates \
                curl \
                gnupg \
                lsb-release
                sudo mkdir -p /etc/apt/keyrings
                curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
                echo \
                "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
                $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
                sudo apt-get update
                sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
                '''

            }
        }

    stage("Testing Stage"){
            steps{
                sh'''
                sudo docker pull nginx
                sudo docker run --name webserver -d -p 81:80 nginx:latest
                '''
            }
        }
    }
}
