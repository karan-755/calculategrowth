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
                sh "docker build . -t calculategrowthapp:1.0.0"
				echo "docker build . -t DockerImageName:TagName"
            }
        }
        stage("Docker Run"){
            steps{
                sh"docker run -p 8501:8501 calculategrowthapp" 
				echo "docker run -p ServerPort:ContainerPort DockerImageName"
                }
            }
        stage("Push DockerImage to DockrHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/calculategrowthapp:1.0.0"
					echo "docker push DOCKER_HUB_USERNAME/DockerImageName:TagName"
				}
			}
		}
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                }
            }
        }
    }
