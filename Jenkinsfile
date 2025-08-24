pipeline {
    agent { label 'dev' }   // Jenkins agent with label "dev"

    tools {
        maven 'Maven'   // Configure Maven under "Global Tool Configuration" in Jenkins
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/YourUsername/YourRepo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    echo "Stopping Tomcat..."
                    /opt/tomcat9/bin/shutdown.sh || true

                    echo "Cleaning old WAR..."
                    rm -rf /opt/tomcat9/webapps/petshop*
                    
                    echo "Deploying new WAR..."
                    cp target/petshop.war /opt/tomcat9/webapps/

                    echo "Starting Tomcat..."
                    /opt/tomcat9/bin/startup.sh
                '''
            }
        }
    }

    post {
        success {
            echo "🎉 Deployment Successful!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}

