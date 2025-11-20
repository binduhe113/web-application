pipeline{
    agent any
    
    tools{
        jdk 'java-11'
        maven 'maven'
    }
    
    stages{
        stage('Git-checkout'){
            steps{
                git branch: 'master' , url: 'https://github.com/binduhe113/web-application.git'
            }
        }
        stage('Code Compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Code Package'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Build and tag'){
            steps{
                sh 'docker build -t binduhe113/project-1 .'
            }
        }
        stage('Containerisation'){
            steps{
                sh '''
                docker run -it -d --name c8 -p 9008:8080 binduhe113/project-1
                '''
            }
        }
        stage('Login to Docker Hub') {
                    steps {
                        script {
                             withCredentials([usernamePassword(credentialsId: '8e747a49-7bde-41c6-a498-a6900d48a88e', passwordVariable: 'user_password', usernameVariable: 'user_name')]) {
                             sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                             }
                                
                            }
                        }
                    }
         stage('Pushing image to repository'){
            steps{
                sh 'docker push binduhe113/project-1'
            }
        }
        
    }
}
