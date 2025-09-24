pipeline {
    agent any

    environment {
        MYSQL_ROOT_PASSWORD = credentials('mysql-root-password')
        SPRING_DATASOURCE_PASSWORD = credentials('mysql-root-password')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/mohithsiddiraju/cicdproject.git'
            }
        }

        stage('Prepare .env') {
            steps {
                sh '''
                cat > .env <<EOF
                MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD
                MYSQL_DATABASE=tuneup
                SPRING_DATASOURCE_USERNAME=root
                SPRING_DATASOURCE_PASSWORD=$SPRING_DATASOURCE_PASSWORD
                SERVER_PORT=8080
                EOF
                '''
            }
        }

        stage('Build & Deploy') {
            steps {
                sh '''
                docker compose down -v
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}
