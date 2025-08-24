pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/TriveniLekireddy/pet_shop.git'
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
                  echo "Deploying WAR file to Tomcat..."
                  # Stop Tomcat (optional, sometimes needed)
                  # sudo systemctl stop tomcat

                  # Copy the WAR file to Tomcat webapps
                  sudo cp target/*.war /opt/tomcat9/webapps/

                  # Start Tomcat again (if stopped)
                  # sudo systemctl start tomcat

                  echo "Deployment finished!"
                '''
            }
        }
    }
}


