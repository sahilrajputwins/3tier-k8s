pipeline{
    agent any
    stages{
        stage("Check node"){
            steps{
                sh ''' kubectl get nodes -o wide '''
            }
        }
        stage("Docker Login"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
                    sh '''echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin '''
                }
            }
        }
        stage("Deploy pods"){
            steps{
                sh ''' kubectl apply -f 3tier-app.yaml '''
            }
        }
        stage("Get pods"){
            steps{
                sh ''' kubectl get pods -o wide '''
            }
        }
    }
}