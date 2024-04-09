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
                deployToTomcat(credentialsId: 'tomcat_deploy_credentials', url: 'http://57.151.123.161:8080/', contextPath: 'test', war: '**/*.war')
            }
        }
    }
}

def deployToTomcat(Map params) {
    withCredentials([usernamePassword(credentialsId: params.credentialsId, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
        sh """
            curl -T ${params.war} http://${USERNAME}:${PASSWORD}@${params.url}/manager/text/deploy?path=/${params.contextPath}
        """
    }
}
