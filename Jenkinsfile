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
                    // Deployment steps for the production branch
                    echo "Deploying to production..."
                    // Adjust your deployment steps here
                    deploy adapters: [tomcat9 (
                            credentialsId: 'tomcat_deploy_credentials',
                            path: '',
                            url: 'http://57.151.123.161:8080/'
                        )],
                        contextPath: 'test',
                        onFailure: 'false',
                        war: '**/*.war'
                }
            }
        }
    }
}
