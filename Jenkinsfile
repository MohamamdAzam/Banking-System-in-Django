
pipeline {
    agent any
    
    environment {
        DJANGO_SETTINGS_MODULE = 'Banking-System-in-Django.settings'
        PYTHONPATH = "$WORKSPACE:$WORKSPACE/Banking-System-in-Django"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MohamamdAzam/Banking-System-in-Django.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'python manage.py test'
            }
        }
        
        stage('Collect Static Files') {
            steps {
                sh 'python manage.py collectstatic --noinput'
            }
        }
        
        stage('Database Migrations') {
            steps {
                sh 'python manage.py migrate'
            }
        }
        
        stage('Deploy') {
            steps {
                // Here you would copy your Django project files to your EC2 instance
                // Example:
                sh 'scp -r Banking-System-in-Django/* ubuntu@34.203.239.25:/var/www/Banking-System-in-Django/'
                
                // Restart Django server (assuming you have Django running with a WSGI server)
                // Example:
                sh 'ssh ubuntu@34.203.239.25 "sudo systemctl restart gunicorn"'
            }
        }
    }
    
    post {
        always {
            // Clean up workspace or perform any other post-build tasks
            cleanWs()
        }
    }
}
