pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/Akil2020/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t akil1991/phpappimage:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dock-hub-pat', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push akil1991/phpappimage:v1'
                }
            }
        }
     stage('Deploy') {
            steps {
                    sh 'sudo docker run -itd --name phpwebapp -p 8089:80 akil1991/phpappimage:v1'

                    }
                }
            }
        }
