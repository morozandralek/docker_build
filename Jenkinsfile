pipeline {
    agent {
        label 'node2'
    }
    stages {
        stage('Check stop docker') {
            steps {
                sh """
                cd docker_build
                docker-compose stop
                docker-compose rm -f
                rm -rf ../docker_build/
                """
            }
        }
        stage('Create volumes') {
            steps {
                sh """
                mkdir -p /var/lib/jenkins/path/to/movies
                mkdir -p /var/lib/jenkins/path/to/downloadclient-downloads
                mkdir -p /var/lib/jenkins/path/to/tvseries
                mkdir -p /var/lib/jenkins/www
                """
            }
        }
        stage('GitHub clone config'){
            steps {
                sh """
                git clone https://github.com/morozandralek/docker_build.git
                """
            }
        }
        stage('docker-compose UP'){
            steps{
                sh """
                cd docker_build
                git checkout jenkins
                docker-compose up -d
                """
            }
        }
        stage('Move index.html'){
            steps{
                sh """
                cp docker_build/index.html /var/lib/jenkins/www/
                """
            }
        }
    }
    
    post {
            success {
                slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            }
            failure {
                slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            }
        }    
}
