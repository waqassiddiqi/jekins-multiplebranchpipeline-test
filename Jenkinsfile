pipeline {
    agent any
	options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    
    stages {
        stage('Clean') {
            steps {
                cleanWs()
            }            
        }

        stage('Build') {
            steps {
                dir('jekins-multiplebranchpipeline-test') {
                	// pull the branch that we received an alert for?
                    sh 'printenv'
                    sh "echo ${GIT_BRANCH}"
                    sh "echo ${GIT_COMMITTER_NAME}"
                    git branch: "${GIT_BRANCH}", url: 'https://github.com/waqassiddiqi/jekins-multiplebranchpipeline-test.git'
                    sh "mvn clean install"
                }
            }
        }
    }
}
