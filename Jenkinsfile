pipeline {

    agent any

    stages {

        stage('Create Virtual Environment') {
            steps {
                sh '''
                    python3 --version
                    python3 -m venv venv
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    ./venv/bin/python -m pip install --upgrade pip
                    ./venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Application Test') {
            steps {
                sh '''
                    # Stop any old Flask process
                    pkill -f app.py || true

                    # Start Flask in background
                    ./venv/bin/python app.py > flask.log 2>&1 &

                    # Wait for startup
                    sleep 5

                    # Test Health Endpoint
                    curl http://localhost:5000/health

                    # Test Employees Endpoint
                    curl http://localhost:5000/employees

                    # Stop Flask after testing
                    pkill -f app.py || true
                '''
            }
        }
    }

    post {
        success {
            echo 'Flask application tested successfully!'
        }

        failure {
            echo 'Pipeline execution failed!'
        }

        always {
            sh 'pkill -f app.py || true'
        }
    }
}
