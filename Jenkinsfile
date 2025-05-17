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
                    pip install flask
                    sudo apt-get install -y tmux
                    tmux new-session -d -s flaskapp 'python3 app.py'
                '''
            }
        }
    }
}
