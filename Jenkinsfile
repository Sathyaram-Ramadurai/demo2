pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the repository
                git 'https://github.com/Sathyaram-Ramadurai/demo2.git'
            }
        }

        stage('Package') {
            steps {
                // Create a deployable artifact (e.g., WAR or JAR file)
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application to a web server or container
                sh 'cp target/my-app.war C:/Users/10433/Downloads/apache-tomcat-8.5.89-windows-x64/apache-tomcat-8.5.89/webapps'
            }
        }
    }
}
