pipeline {
    agent any
    stages {
        stage('Test curl') {
            agent {
                label 'node2'
            }
            steps('create mkdir') {
                sh """
                mkdir -p /var/lib/jenkins/path/to/movies
		mkdir -p /var/lib/jenkins/path/to/downloadclient-downloads
		mkdir -p /var/lib/jenkins/path/to/tvseries
                """
            }
            steps('clone repo github'){
		sh """
		git clone git@github.com:morozandralek/docker_build.git
		""" 
            }
	    steps('run docker-compose'){
		sh """
		cd docker_build
		git checkout jenkins
                docker-compose up -d
		"""
            }
        }
    }
}
