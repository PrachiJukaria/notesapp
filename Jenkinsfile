pipeline{
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    
    stages {
        stage("clone code"){
            steps{
                echo "Cloning the code from github"
                git branch: 'main', url: 'https://github.com/PrachiJukaria/notesapp.git'
            }
        }
        
        stage("Build"){
            steps{
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        
        // stage("Pushing to docker hub"){
        //     steps{
        //         echo("Pushing to docker hub")
        //         withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
        //             sh "docker tag my-note-app ${env.dockerhubUser}/my-note-app:latest"
        //             sh('echo $env.dockerhubPass | docker login -u $env.dockerhubUser --password-stdin')
        //             sh "docker push ${env.dockerhubUser}/my-note-app:latest"
        //         }
        //     }
        // }
        
        stage("deploy"){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
