pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Set Up Python Virtual Environment and Run App') {
            steps {
                sh '''
                    echo "Updating system and installing python3-venv..."
                    sudo apt-get update
                    sudo apt-get install -y python3-venv

                    echo "Creating Python virtual environment..."
                    python3 -m venv venv

                    echo "Activating virtual environment and installing dependencies..."
                    source venv/bin/activate
                    pip install --upgrade pip
                    pip install pm2

                    echo "Starting the Flask application using PM2..."
                    pm2 start app.py --name flask-app --interpreter ./venv/bin/python3
                    pm2 save
                '''
            }
        }
    }
}
