pipeline {
    agent any
        stages{
        stage("Code"){
            steps{
                git url: "https://github.com/kshitijabartakke/calculategrowth.git", branch: "main"
            }
        }
        stage("Build & Test"){
        }
        stage("Docker Run"){
        }
        stage("Push DockerImage to DockrHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/calculategrowthapp:latest"
					echo "docker push DOCKER_HUB_USERNAME/DockerImageName:TagName"
				}
			}
		}
        stage("Deploy"){
            }
        }
    }
