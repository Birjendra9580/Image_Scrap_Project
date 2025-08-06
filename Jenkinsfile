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
                sh 'docker run -itd -p 0000:8000 my-app:3.0'
            }
        }
        stage("Docker-hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'vishal',passwordVariable: 'PASSWORD',usernameVariable: 'USER')]){
                    sh 'docker login -u $USER -p $PASSWORD'
                    sh 'docker tag my-app:3.0 $USER/my-app:3.0'
                    sh 'docker push $USER/my-app:3.0'
                    sh 'docker logout'
                } 
            }
        }
    }
}
