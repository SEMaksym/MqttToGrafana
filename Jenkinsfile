pipeline {
    agent any
	
    
    stages {
        stage('Start') {
            steps {
                echo 'Lab_2: nginx/custom'
            } 
        }
        
        stage('Image Build') {
            steps {
                sh "docker compose build" 
            } 
        }
        stage('Stop previous artifact'){
		    steps {
                sh "docker compose down -v"
				sh "docker rm -f $(docker ps -a -q)"
				sh "docker volume rm $(docker volume ls -q)"
            } 
		}
        stage('Deploy new artifact'){
            steps{
                sh "docker compose up -d"
            } 
        } 
		stage('Test'){
		    steps{
                sh "mosquitto_pub -d -t 'build/status' -m 'succses'"
			}
		}
        
    } 

}