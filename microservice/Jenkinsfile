pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        BUILD_DIR = "built"
        REPO_URL = "https://github.com/mathew512/springboot-java.git"
        BRANCH = "main"
        PROJECT_DIR = "springboot-java"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}",
                    credentialsId: 'jenkins-github-creds',
                    url: "${REPO_URL}"
            }
        }

        stage('Build with Maven') {
            steps {
                dir("${PROJECT_DIR}") {
                    // Ensure Maven is available on Jenkins agent
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Create built Directory') {
            steps {
                sh '''
                    mkdir -p ${BUILD_DIR}
                    cp ${PROJECT_DIR}/target/*.jar ${BUILD_DIR}/
                '''
            }
        }
    }

    post {
        success {
            echo "Build successful. .jar stored in built/"
            archiveArtifacts artifacts: 'built/*.jar', fingerprint: true
        }
        failure {
            echo "Build failed"
        }
    }
}