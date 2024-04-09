pipeline {
    agent any

    stages {
        stage('Build and Test') {
            steps {
                script {
                    // Build and test steps for both branches
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Install or Deploy') {
            when {
                branch 'development'
            }
            steps {
                script {
                    // Install stage for the development branch
                    // Assuming you have configured Tomcat on the Jenkins node
                    // Adjust the deployment steps according to your setup
                    sh 'mvn install'
                }
            }
        }
        
        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                script {
                    echo "Deploying to Production"
                    // Assuming you have the 'Tomcat_deploy' credentials configured in Jenkins
                    // Adjust the URL, context path, and war file path according to your setup
                    deploy adapters: [tomcat9(
                        credentialsId: 'Tomcat_deploy',
                        url: 'http://57.151.123.161:8088/',
                        war: '**/*.war',
                        contextPath: 'test'
                    )],
                    onFailure: 'false'
                }
            }
        }
    }
}
