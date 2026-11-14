pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Python Build & Test') {
            steps {
                sh '''
                    # 1. Create a virtual environment
                    python3 -m venv venv

                    # 2. Activate virtual environment
                    . venv/bin/activate

                    # 3. Upgrade pip & install dependencies
                    pip install --upgrade pip
                    if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

                    # 4. Run tests or Python script
                    pytest
                    # or: python3 main.py
                '''
            }
        }
    }

    post {
        always {
            // Clean up virtual environment after build
            sh 'rm -rf venv'
        }
    }
}
