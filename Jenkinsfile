pipeline {

    agent {label "dev"}

    stages {

        stage('Code') {

            steps {

                git url: "https://github.com/SUDARSHAN75-lab/two-tier-flask-app.git", branch: "master"

                echo "Code clone ho gaya"

            }

        }

        stage('Build') {

            steps {

                sh "docker build -t two-tier-flask-app ."

                echo "Code Build Ho gaya"

            }

        }

        stage('Test') {

            steps {

                echo " Code Test Ho gaya "

            }

        }

        stage('Push to Docker Hub') {

            steps {

                withCredentials([usernamePassword(

                    credentialsId:"dockerHubCreds",

                    passwordVariable: "dockerHubPass",

                    usernameVariable: "dockerHubUser"

                )]){

                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"

                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"

                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest "

                }

            }

        }

        stage('Deploy') {

            steps {

                sh "docker compose up -d --build flask-app"

                echo " Code Build ho gaya "

            }

        }

    }

}

 
