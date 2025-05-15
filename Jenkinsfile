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

                    echo "Creating virtual environment in /opt/venv..."
                    sudo python3.12 -m venv /opt/venv
                    sudo chown -R $(whoami):$(whoami) /opt/venv

                    echo "Activating virtual environment and installing Flask..."
                    /opt/venv/bin/pip install --upgrade pip
                    /opt/venv/bin/pip install flask

                    echo "Running app.py in background from $(pwd)..."
                    APP_PATH="$(pwd)/app.py"

                    # Log environment info
                    echo "Using Python: $(/opt/venv/bin/python --version)"
                    echo "App path: $APP_PATH"
                    
                    # Launch app with setsid and absolute path
                    setsid /opt/venv/bin/python "$APP_PATH" > app.log 2>&1 < /dev/null &

                    # Save the process ID
                    echo $! > app.pid

                    # Confirm process start
                    sleep 2
                    if ps -p $(cat app.pid) > /dev/null; then
                        echo "App started successfully with PID $(cat app.pid)"
                    else
                        echo "App failed to start. Check app.log for errors."
                        cat app.log
                        exit 1
                    fi
                '''
            }
        }
    }
}
