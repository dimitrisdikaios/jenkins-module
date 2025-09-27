#!/user/bin/env groovy

library identifier: 'jenkins-shared-library@main', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/dimitrisdikaios/jenkins-shared-library.git',
    credentialsId: 'github'])
def gv

pipeline{
    agent any
    tools {
        maven 'maven-3.9'
    }
    stages{
        stage("init"){
            steps {
                script{
                    gv = load 'script.groovy'
                }
            }
        }

        stage("build jar"){
            steps {
                script{
                    buildJar()
                }
            }
        }

        stage("build and push docker image"){
            steps {
                script{
                    buildImage 'dimitrisdikaios/demo-app:jma-4.0'
                    dockerLogin()
                    dockerPush 'dimitrisdikaios/demo-app:jma-4.0'
                }
            }
        }
        
        stage("deploy"){
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
    
}
