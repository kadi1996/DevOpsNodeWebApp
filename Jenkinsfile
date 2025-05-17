pipeline {
    agent any

    stages {
        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DockerHub-kadi1996-DevOps', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            export DOCKER_HOST=tcp://localhost:2375
                            export PATH=$PATH:/usr/local/bin
                            docker login -u $USERNAME -p $PASSWORD
                            docker push kadi96/node-web-app
                        '''
                    }
                }
            }
        }

        stage('Trigger Render Deployment') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'RenderDeployKey', variable: 'KEY')]) {
                        sh '''
                            curl https://api.render.com/deploy/$KEY
                        '''
                    }
                }
            }
        }
    }
}
