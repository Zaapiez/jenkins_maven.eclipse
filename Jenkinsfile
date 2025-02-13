pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9'
        jdk 'Java JDK 17'
    }
    
    environment {
        SONAR_HOST_URL = 'http://localhost:9000' // Replace with your SonarQube server URL
        SONAR_TOKEN = 'jenkin token' // Use Jenkins credentials instead of hardcoding
    }

    stages {
        stage("clean") {
            steps {
                echo "Start Clean"
                bat "mvn clean"
            }
        }
        
        stage("test") {
            steps {
                echo "Start Test"
                bat "mvn test"
                
                echo "Running SonarQube Analysis"
                bat "mvn sonar:sonar -Dsonar.projectKey=jenkins_maven.eclipse -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.login=${SONAR_TOKEN}"
            }
        }
        
        stage("build") {
            steps {
                echo "Start Build"
                bat "mvn install -DskipTests"
            }
        }
    }
}
