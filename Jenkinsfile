// jenkinsfile
pipeline {
        agent any
        enviroment {
                DOCKERHUB_CREDS = credentials('docker')
        }
        stages {
                stage ('docker image build') {
                        steps {
                                sh 'docker build --tag oracle117/cw2-server:0.1'
                        }
                }
                stage ('test image') {
                        steps{
                                sh '''
                                        docker image inspect oracle117/cw2-server:0.1
                                        docker run --name test-container -p 8081:8080 -d oracle117/cw2-server:0.1
                                        docker ps
                                        docker stop test-container
                                        docker rm test-container
                                '''
                        }
                }



                stage('login') {
                        steps {
                                sh 'echo $DOCKERHUB_CREDS_PSW docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
                        }
                }

                stage ('push') {
                        steps {
                                ssh 'docker push oracle117/cw2-server:0.1'
//              stage('deploy') {
//                      steps {
//                              sshagent(['my-ssh-key']) {
//                                      sh 'scp /Users/oracle117/home/aws/'
//                                      }
//                              }
                        }
                }
        }
}





