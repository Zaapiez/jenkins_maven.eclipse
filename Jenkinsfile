pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9'
        jdk 'Java JDK 17'
    }
    
    environment {
        SONAR_SCANNER_HOME = tool 'SonarQube Scanner' 
        SONAR_HOST_URL = 'http://localhost:9000'
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
            }
        }
        
        stage("sonarqube analysis") {
            steps {
                echo "Running SonarQube Analysis"
                bat "${SONAR_SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=your_project_key -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.login=your_sonar_token"
            }
        }
        
        stage("build") {
            steps {
                echo "Start build"
                bat "mvn install -DskipTests"
            }
        }
    }
}
