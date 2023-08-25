pipeline {
    agent any
        stages{
        stage("Code"){
            steps{
                git url: "https://github.com/kshitijabartakke/calculategrowth.git", branch: "main"
            }
        }
        stage("Build & Test"){
            steps{
				echo "Build and Test"
				withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker build -t kshitibartakke/calculategrowth ."
					echo "docker push DOCKER_HUB_USERNAME/DockerImageName:TagName" 
					}
            }
        }
        stage("Docker Run"){
            steps{
				echo "Docker Run"
				sh "docker run -p 8501:8501 kshitibartakke/calculategrowth"
                }
            }
        stage("Push DockerImage to DockrHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker images"
					sh "docker push kshitibartakke/calculategrowth:latest"
				}
			}
		}
        stage("Deploy"){
            steps{   
				echo "Deploy"            
                }
            }
        }
    }
