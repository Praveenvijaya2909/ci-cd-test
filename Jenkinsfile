pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repo...'
            }
        }

        stage('Set Up Python in /opt') {
            steps {
                sh '''
                    sudo apt-get update
                    sudo apt-get install -y python3.12-venv

                    # Create virtual environment in /opt
                    sudo python3.12 -m venv /opt/venv

                    # Change ownership so Jenkins can access it
                    sudo chown -R $(whoami):$(whoami) /opt/venv

                    # Activate environment and install dependencies
                    . /opt/venv/bin/activate
                    pip install flask

                    # Run the app in background
                    nohup /opt/venv/bin/python app.py > app.log 2>&1 < /dev/null &
                '''
            }
        }
    }
}
