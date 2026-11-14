pipeline {

    agent any

    stages {

        stage('Check Python') {

            steps {

                sh 'python3 --version'

            }

        }

        stage('Create Virtual Environment') {

            steps {

                sh '''

                    python3 -m venv venv

                    venv/bin/python -m pip install --upgrade pip

                '''

            }

        }

        stage('Install Dependencies') {

            steps {

                sh '''

                    venv/bin/pip install -r requirements.txt

                '''

            }

        }

        stage('Run Flask Application') {

            steps {

                sh '''

                    venv/bin/python -c "import flask; print('Flask installed successfully')"

                '''

            }

        }

    }

    post {

        success {

            echo 'Pipeline executed successfully!'

        }

        failure {

            echo 'Pipeline execution failed!'

        }

    }

}
