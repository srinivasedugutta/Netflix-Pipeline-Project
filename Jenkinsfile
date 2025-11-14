pipeline {
    agent any
    
    tools {
        maven 'maven3'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/srinivasedugutta/Netflix-Pipeline-Project.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package -T 1C -DskipTests'
            }
        }
        stage('Artifact Download') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                sh 'sudo cp target/NETFLIX-1.2.2.war /home/ec2-user/apache-tomcat-9.0.112/webapps'
            }
        }
    }
}
