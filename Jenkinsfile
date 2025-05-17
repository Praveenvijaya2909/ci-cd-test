pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repo...'
                // You should include the actual git checkout step here.
            }
        }

        stage('Set Up Python in /opt and Run App') {
            steps {
                sh '''
                    echo "Updating system and installing Python venv..."
                    sudo apt-get update
                    sudo apt-get install -y python3.12-venv

                    . venv/bin/activate
                    pip install pm2
                    pm2 start app.py --name flask-app --interpreter python3
                    pm2 save
                '''
            }
        }
    }
}
