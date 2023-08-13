pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}

// This is my Jenkinsfile
// pipeline{
//     agent any
//     stages{
//         stage("Code"){
//             steps{
//             echo "Cloning the Code"
//             git url:"https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
//             }
//         }
//         stage("build"){
//             steps{
//             echo "Building the Code"
//             sh "docker build -t my-dev-app:latest ."
            
//             }
//         }
//         stage("Push to DockerHub"){
//             steps{
//             echo "Pushing to Image to DockerHUB" 
            
//             withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
//             sh "docker tag my-devops-app $USERNAME/my-devops-app:latest"
//             sh "docker login -u $USERNAME -p $PASSWORD"
//             sh 'echo $PASSWORD'
            
//             // echo USERNAME 
//             echo "username is $USERNAME"
//             sh "docker push $USERNAME/my-devops-app:latest"
//             }
//             }
//         }
//         stage("Deploy"){
//             steps{
//             echo "Deplying the container"
//             sh "docker run -d -p8000:8000 anu374/my-devops-app:latest"
//             }
//         }
//         stage("Git push"){
//             steps{
//                 echo "Git pushing"
//                 withCredentials([usernamePassword(credentialsId: 'Github', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
//                 sh "docker tag my-devops-app $USERNAME/my-devops-app:latest"
//                 sh "git branch -m main master"
//                 sh "git fetch origin"
//                 sh "git branch -u origin/master master"
//                 sh "git remote set-head origin -a"
//                 }
//             }
//         }
//     }
    
// }
