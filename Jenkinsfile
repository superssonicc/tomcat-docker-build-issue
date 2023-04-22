pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Create Tomcat Docker Image'){
            steps{
                sh "sudo usermod -aG docker ${USER}"
                sh "sudo systemctl restart docker"
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }
    }
}