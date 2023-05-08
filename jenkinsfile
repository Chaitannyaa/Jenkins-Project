pipeline {
    agent prod
    stages {
        stage ("code"){
            steps {
                git url: 'https://github.com/Chaitannyaa/Jenkins-Project.git', branch: 'production'
            }
        }
        stage ("Build docker images"){
            steps {
                sh 'docker build -t chaitannyaa/multi_container_app:worker .'
                sh 'docker build -t chaitannyaa/multi_container_app:result .'
                sh 'docker build -t chaitannyaa/multi_container_app:vote .'
            }
        }
        stage("Deploy services"){
            steps {
                 sh "docker-compose down && docker-compose up -d"
            }
        }        
        stage ("Update docker images"){
            steps {
                echo 'Logging into DockerHub and pushing an image on DockerHub'
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'password', usernameVariable: 'user')]) {
                    sh "docker login -u ${env.user} -p ${env.password}"
                    sh "docker push chaitannyaa/multi_container_app:worker"
                    sh "docker push chaitannyaa/multi_container_app:result"
                    sh "docker push chaitannyaa/multi_container_app:vote"
                }
            }
        }
        stage('Notify Management team') {
            steps {
                // Send a notification email to the team
                echo "The latest versions of the microservices has been deployed to the production environment." | mail -s "Microservices are deployed successfully!" -a "From: DevOps-Chaitannyaa Gaikwad" chaitannyaagaikwad@gmail.com
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
