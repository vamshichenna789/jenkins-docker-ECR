pipeline { 
    agent any 
    stages { 
         stage('Clone repository') {  
            steps {  
                script{ 
                checkout scm 
                } 
            } 
        } 
        stage('Build') {  
            steps {  
                script{ 
                    app = docker.build("docker-demo:${env.BUILD_ID}") 
                } 
            } 
        } 
        stage('Test'){ 
            steps { 
                sh 'trivy image docker-demo:${env.BUILD_ID} || exit 0' 
            } 
        } 
        stage('Deploy') { 
            steps { 
                script{ 
                        docker.withRegistry('https://311288273862.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:ecrtocken') { 
                    app.push() 
                    } 
                } 
            } 
        } 
    } 
}
