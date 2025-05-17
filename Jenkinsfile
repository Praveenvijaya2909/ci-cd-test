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
                    pip install flask
                    sudo apt-get install -y tmux
                    tmux new-session -d -s flaskapp 'python3 app.py'
                '''
            }
        }
    }
}
