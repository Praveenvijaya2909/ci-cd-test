pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repo...'
            }
        }

        stage('Set Up Python') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install pm2
                    pip install flask
                    pm2 start app.py --name flask-app --interpreter python3
                    pm2 save
                '''
            }
        }   
    }
}
