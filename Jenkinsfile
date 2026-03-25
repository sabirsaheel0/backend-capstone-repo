pipeline {
    agent any

    stages {

        stage('BUILD DOCKER IMAGE') {
            steps {
                echo 'building docker image........'
                sh 'docker build -t sabirsaheel0/backend-capstone:${BUILD_NUMBER} .'
            }
        }

        stage('DOCKER LOGIN + PUSH') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    passwordVariable: 'pass',
                    usernameVariable: 'uname'
                )]) {
                    sh 'echo ${pass} | docker login -u ${uname} --password-stdin'
                }

                sh 'docker push sabirsaheel0/backend-capstonet:${BUILD_NUMBER}'
                sh 'docker logout'
                echo 'pushing docker image'
            }
        }

        stage('clean docker images') {
            steps {
                sh 'docker rmi sabirsaheel0/backend-capstone:${BUILD_NUMBER}'
            }
        }

    }
}