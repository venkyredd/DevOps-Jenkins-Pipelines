
pipeline {
    agent any

    environment {
        APP_DIR = "/home/ubuntu/nodejs-app"
        EC2_USER = "ubuntu"
        EC2_HOST = "3.110.207.48"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/venkyredd/DevOps-Jenkins-Pipelines.git'
            }
        }

        stage('Deploy to EC2') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: '58658932-14f2-403a-a881-91785c3fbf94', keyFileVariable: 'SSH_KEY')]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no -i $SSH_KEY $EC2_USER@$EC2_HOST "
                        mkdir -p $APP_DIR;
                        cd $APP_DIR;
                        git pull origin main;
                        npm install;
                        pm2 stop all;
                        pm2 start server.js;
                        "
                    """
                }
            }
        }
    }
}
