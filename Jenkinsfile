pipeline {

    environment{
        dockerRepo = 'vadimdo93'
    }
    
    agent any

    stages{

        stage("Docker image build") {
            steps {
                sh 'docker build -t $dockerRepo/py-app:$BRANCH_NAME.$BUILD_NUMBER -f docker/Dockerfile .'
                sh 'docker images'
            }
        }

        stage("Pushing docker image") {

            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')
                ]){
                sh "docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}"
                sh "docker push $dockerRepo/py-app:$BRANCH_NAME.$BUILD_NUMBER"
                sh "docker rmi $dockerRepo/py-app:$BRANCH_NAME.$BUILD_NUMBER"
                }
            }
        }
    }
}
