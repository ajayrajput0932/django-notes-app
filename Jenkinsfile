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
        
       stage("Push") {
    steps {
        echo "Pushing images to Docker Hub..."

        withCredentials([
            usernamePassword(
                credentialsId: "ajaybanna",
                usernameVariable: "DOCKER_USER",
                passwordVariable: "DOCKER_TOKEN"
            )
        ]) {
            sh '''
                echo "$DOCKER_TOKEN" | docker login -u "$DOCKER_USER" --password-stdin

                docker push "$DOCKER_USER/notes-nginx:latest"
                docker push "$DOCKER_USER/django-notes-app:latest"

                docker logout
            '''
        }
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
