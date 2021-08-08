pipeline {

    agent any

    stages{

        stage("Docker image build") {
            steps {
                sh 'docker build -t py-app:1.0 -f docker/Dockerfile .'

            }
        }

        stage("Pushing docker image") {

            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')
                ]){
                sh "docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}"
                sh "docker push ${DOCKER_USER}/py-app:1.0"
                }
            }
        }
    }
}
