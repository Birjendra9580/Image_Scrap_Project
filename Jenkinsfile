pipeline{
    agent any
    stages{
        stage("checkout"){
            steps{
                checkout scm
            }
        }
        stage("Build Image"){
            steps{
                sh 'docker build -t my-app:3.0 .'
                sh 'docker run -itd -p 8000:8000 my-app:3.0'
            }
        }
        stage("Docker-hub"){
           steps{
                withCredentials([usernamePassword(credentialsId: 'vishal',passwordVariable: 'password',usernameVariable: 'user')]){
                     sh 'docker login -u $user -p password'
                     sh 'docker tag my-app:3.0 $user/my-app:3.0'
                     sh 'docker push $user/my-app:3.0'
                     sh 'docker logout'
                } 
            }
        }
    }
}
