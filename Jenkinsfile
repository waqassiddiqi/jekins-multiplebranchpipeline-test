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
                	
                    sh 'printenv'

                    checkout resolveScm source: [$class: 'GitSCMSource', credentialsId: 'Github-Creds', id: '_', remote: 'https://github.com/waqassiddiqi/jekins-multiplebranchpipeline-test.git', traits: [[$class: 'jenkins.plugins.git.traits.BranchDiscoveryTrait']]], targets: ['dev, develop']
                    
                    script {
                        GIT_CULPRIT = sh(returnStdout: true, script:'git --no-pager show -s --format=%ae | sed s/[@].*//').trim()
                        echo "culprit: ${GIT_CULPRIT}"
                    }

                    // git branch: "${GIT_BRANCH}", url: 'https://github.com/waqassiddiqi/jekins-multiplebranchpipeline-test.git'
                    sh "mvn clean install"
                }
            }
        }
    }
}
