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
                    sh 'mvn install'
                }
            }
            
            when {
                branch 'main'
            }
            steps {
                script {
                    // Deploy stage for the main branch
                    // Assuming you have configured Tomcat on the Jenkins node
                    // Adjust the deployment steps according to your setup
                    sh 'sudo cp /home/azureuser/Project7---Deploying-a-Java-Web-Application-into-Kubernetes-Cluster-using-Ansible/webapp/target/webapp.war /opt/tomcat/latest/webapps/'
                    sh 'sudo systemctl restart tomcat'
                }
            }
        }
    }
}
