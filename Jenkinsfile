pipeline{
    agent any
    tools {
        maven 'maven-3.9'
    }
    stages{
        stage("build jar"){
            steps {
                script{
                    echo "building the application..."
                    sh 'mvn package'
                }
            }
        }

        stage("build docker image"){
            steps {
                script{
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t dimitrisdikaios/demo-app:jma-2.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push dimitrisdikaios/demo-app:jma-2.0'
                    }
                }
            }
        }

        stage("deploy"){
            steps {
                script {
                    echo "deploying the application..."
                }
            }
        }
    }
    
}
