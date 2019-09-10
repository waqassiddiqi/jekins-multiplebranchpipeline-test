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
                	script {
                        def branch = resolveScm source: [$class: 'GitSCMSource', credentialsId: 'Github-Creds', id: '_', remote: 'https://github.com/waqassiddiqi/jekins-multiplebranchpipeline-test.git', traits: [[$class: 'jenkins.plugins.git.traits.BranchDiscoveryTrait']]], targets: ['dev', GIT_BRANCH]
                        checkout branch
                        sh "ls"
                        sh "mvn clean install"
                    }
                }
            }
        }
    }
}
