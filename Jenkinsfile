pipeline {
    agent {
        label 'node2'
    }
    stages {
        stage('create mkdir') {
            steps {
                sh """
                mkdir -p /var/lib/jenkins/path/to/movies
                mkdir -p /var/lib/jenkins/path/to/downloadclient-downloads
                mkdir -p /var/lib/jenkins/path/to/tvseries
                """
            }
        }
        stage('clone repo github'){
            steps {
                sh """
                git clone https://github.com/morozandralek/docker_build.git
                """
            }
        }
        stage('run docker-compose'){
            steps{
                sh """
                cd docker_build
                git checkout jenkins
                docker-compose up -d
                """
            }
        }
    }
}
