pipeline {


    agent any

    stages {


        stage('Install Dependencies') {
    steps {
        sh '''
            python3 -m venv .venv
            .venv/bin/pip install --upgrade pip
            .venv/bin/pip install -r requirements.txt
        '''
    }
}
stage('Test Flask Application') {
    steps {
        sh '''
            # 1. Start Flask in the background
            .venv/bin/python app.py &
            FLASK_PID=$!
            # 2. Give it a moment to boot up
            sleep 3
            # 3. Test that it responds
            curl -I http://127.0.0.1:5000
            # 4. Gracefully terminate Flask so Jenkins can proceed
            kill $FLASK_PID
        '''
    }
}
    }


    post {
        success {
            echo 'Flask application started successfully!'
        }


        failure {
            echo 'Pipeline execution failed!'
        }
    }
}
