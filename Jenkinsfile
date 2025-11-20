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
                docker run -it -d --name tomcat -p 9001:8080 binduhe113/project-1
                '''
            }
        }
        stage('Login to Docker Hub') {
                    steps {
                        script {
                            withCredentials([usernamePassword(credentialsId: 'docker_new', passwordVariable: 'user_password', usernameVariable: 'user_name')]) {
                            sh "echo $user_password | docker login -u $user_name --password-stdin"
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
