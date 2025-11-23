@Library("shared") _
pipeline{
    agent{label "vinod"}
    stages{
        stage("hello-"){
            steps{
              script{
                    hello()
                }
                }
            }
        
        stage("git clone-stage"){
            steps{
            // echo "now git clone start------->"
            // git url: "https://github.com/sumit26-lab/Portfolio-React-Tailwind-Ci-cd-ec2.git",branch:"main"
            script{
                github_clone("https://github.com/sumit26-lab/Portfolio-React-Tailwind-Ci-cd-ec2.git","main")
            }
            }
                
            }

        stage("code-build"){
            steps{
                script{
                    
                    docker_build("sumitsinghchouhan","vite-jenkins-portfolio","latest")
                }
                //  echo "now docker build Code start------->"
                //  sh "docker build -t portfolio-reactapp:latest ." 
                // echo "now docker build Created SuccessFuily !!"
           
            }
           
        }
         stage("Docker Image Push on docker-registry"){
            steps{
                script{
                    
                    docker_push("sumitsinghchouhan","vite-jenkins-portfolio","latest")
                }
                // echo "now docker image push on docker Hub & Registry !!"
                // withCredentials([usernamePassword(credentialsId: 'dockerhubCred', 
                // usernameVariable: 'DOCKER_HUB_USER',
                // passwordVariable: 'DOCKER_HUB_PASS')]) {
                
                // // loginDocker hub
                // sh "docker login -u ${env.DOCKER_HUB_USER} -p ${env.DOCKER_HUB_PASS}"
                // // create image tage
                // sh "docker image tag portfolio-reactapp:latest ${env.DOCKER_HUB_USER}/vite-jenkins-portfolio:latest"
                // // push on hub
                // sh "docker push ${env.DOCKER_HUB_USER}/vite-jenkins-portfolio:latest"
                // echo "image on push docker hub"
                
                
            }
        }
        stage("Deploye-to Ec2"){
         
             steps{
              echo "start to deployement"
        //     //  sh "docker run -d -p 80:80 portfolio-reactapp:latest"
                 sh """
                  docker-compose --version
                  """
                  sh "sudo apt-get install docker-compose-v2"
              
             sh "docker compose down && docker compose up -d"
             }
         }
        
        
        
    }
}
