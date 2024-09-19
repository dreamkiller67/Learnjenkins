pipeline {
    agent any
    environment {
        // Define environment variables
        IMAGE_NAME = 'dasnarayanb2/restapp'
        PORT_MAPPING = '9090:8181'
        CONTAINER_NAME = 'ajay'
        TAG = "${BUILD_NUMBER}"
    }
    
    stages {

        stage('clean-up'){
            steps{
                sh 'rm -rf RestApp'
            }
        }
        
        stage('git-clone') {
            steps {
                sh 'git clone https://github.com/dreamkiller67/RestApp.git'
            }
        }
 
        
        stage('mvn-package') {
            steps {
               sh 'cd /var/lib/jenkins/workspace/HelloDevOps/RestApp && mvn package'
            }
        }
        
        stage('image-creation') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/HelloDevOps/RestApp && docker push dasnarayanb2/restapp'
            }
        }
        
        
        // Deploy stage starts here
        stage('Deploy') {
            steps {
                // Deploy the Docker image to your environment (e.g., Kubernetes, Docker Swarm)
                sh '''if [ "$(docker ps -aq -f name=$CONTAINER_NAME)" ]; then
                         echo "Stopping and removing existing container..."
                         docker stop $CONTAINER_NAME
                         docker rm $CONTAINER_NAME
                   fi'''
                sh 'docker run -d -p 9090:8181 --name $CONTAINER_NAME dasnarayanb2/restapp'
            }
        }
     // Deploy stage ends here
        
        
    }
}

