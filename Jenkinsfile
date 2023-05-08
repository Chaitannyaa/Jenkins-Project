pipeline {
    agent {
        label 'release'
    }
    environment {
        DOCKER_IMAGE_TAG = "${BUILD_NUMBER}"
    }
    stages {
        stage ("code"){
            steps {
                git url: 'https://github.com/Chaitannyaa/Jenkins-Project.git', branch: 'release-1.1'
            }
        }
        stage ("Build docker images"){
            steps {
                sh 'docker build -t chaitannyaa/multi_container_app:worker-R-${DOCKER_IMAGE_TAG} .'
                sh 'docker build -t chaitannyaa/multi_container_app:result-R-${DOCKER_IMAGE_TAG} .'
                sh 'docker build -t chaitannyaa/multi_container_app:vote-R-${DOCKER_IMAGE_TAG} .'
            }
        }
        stage("Deploy services"){
            steps {
                 sh "docker-compose down && docker-compose up -d"
            }
        }        
        stage ("Update docker images"){
            steps {
                echo 'Logging into docker and pushing an image on dockerhub'
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'password', usernameVariable: 'user')]) {
                    sh "docker login -u ${env.user} -p ${env.password}"
                    sh "docker push chaitannyaa/multi_container_app:worker-R-${DOCKER_IMAGE_TAG}"
                    sh "docker push chaitannyaa/multi_container_app:result-R-${DOCKER_IMAGE_TAG}"
                    sh "docker push chaitannyaa/multi_container_app:vote-R-${DOCKER_IMAGE_TAG}"
                }
            }
        }
        stage('Notify Management team') {
            steps {
                // Send a notification email to the team
                sh 'echo "The latest versions of the microservices has been deployed to the Version-tesing environment." | mail -s "New versions are deployed successfully!" -a "From: DevOps-Chaitannyaa Gaikwad" chaitannyaagaikwad@gmail.com'
            }
        }
        stage("Clean-up"){
            steps {
                sh '''
                set +e
                docker rmi -f $(docker images -a -q)
                if [ $? -eq 0 ]; then
                    echo "All Docker images have been removed successfully."
                else
                    echo "Error: Could not remove all Docker images."
                fi
                set -e
                '''
            }
        }        
    }
}
