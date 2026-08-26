pipeline {
    agent { label "ubuntu" }

    stages {

        stage("Code") {
            steps {
                echo "Cloning code..."
                git url: "https://github.com/ajayrajput0932/django-notes-app.git",
                    branch: "main"
            }
        }

        stage("Build") {
            steps {
                echo "Building Docker images..."
                sh "docker compose build"
            }
        }

        stage("Test") {
            steps {
                echo "Testing application..."
                sh "docker compose config"
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying application..."

                sh "docker compose down"
                sh "docker compose up -d --build"
            }
        }
    }
}
