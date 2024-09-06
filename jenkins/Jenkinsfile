pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                script {
                    // Ensure that the script file has executable permissions
                    sh 'chmod +x /var/jenkins_home/workspace/*/jenkins/scripts/deliver.sh'
                }
                // Execute the script
                sh './jenkins/scripts/deliver.sh'
            }
        }
        stage('Complete') {
            steps {
                echo 'Job Complete!'
            }
        }
    }
}
