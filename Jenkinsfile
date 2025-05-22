pipeline {
    agent any
    tools {
        gradle 'gradle'
        jdk 'jdk17'
    }
  environment {
        SONAR_TOKEN = credentials('sonar-token') // Jenkins credential ID
        SONAR_HOST_URL = 'https://682f562ba0474eb779d91a3f-6fa094.node-ap-a1de.iximiuz.com'
        SONAR_SCANER_HOME= tool 'SonarQube'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'develop', url: 'https://github.com/Shopping-App-Services/ad-service.git'
            }
        }
        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew downloadRepos'
                sh './gradlew installDist'
                sh '''
                    echo "--- Verifying .class files exist ---"
                    find build/classes/java/main -name "*.class" || true
                
                    echo "--- Showing current working directory ---"
                    pwd
                
                    echo "--- Listing files in root ---"
                    ls -l
                
                    echo "--- Listing files in build/classes/java/main ---"
                    ls -l build/classes/java/main
            '''
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                     sh '''
                    ${SONAR_SCANER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=AdService \
                        -Dsonar.sources=src/main/java \
                        -Dsonar.inclusions=src/main/java/**/*.java \
                        -Dsonar.java.binaries=build/classes/java/main \
                        -Dsonar.sourceEncoding=UTF-8 \
                        -Dsonar.host.url=$SONAR_HOST_URL \
                        -Dsonar.verbose=true
                    '''
                    }  
                }
            }
        }
        stage("Quality Gate") {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        stage("Docker Build & Push") {
            steps {
                script {
                    // This step should not normally be used in your script. Consult the inline help for details.
                   withDockerRegistry(credentialsId: 'fb045f21-4646-4b13-9a81-aae491da4b94', toolName: 'docker') {
                        sh 'ls -latr'
                        sh "docker build -t ad-service ."
                        sh "docker tag ad-service nitesh2611/ad-service:latest "
                        sh "docker push nitesh2611/ad-service:latest "
                    }
                }
            }
        }
    }
}


