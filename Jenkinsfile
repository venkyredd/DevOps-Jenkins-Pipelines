pipeline {
    agent any

    environment {
        APP_DIR = "/home/ubuntu/react-app"
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
                        cd $APP_DIR &&
                        git pull origin main &&
                        npm install &&
                        npm run build &&
                        sudo cp -r build/* /var/www/html/
                        "
                    """
                }
            }
        }
    }
}
