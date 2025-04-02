pipeline {
    agent {
        label 'openshift'
    }
    
    environment {
        OPENSHIFT_SERVER = 'https://api.rm2.thpm.p1.openshiftapps.com:6443'
        OPENSHIFT_NAMESPACE = "amritasaha11111-dev"
        GIT_REPO_URL = 'https://github.com/Amritaint/INT.git'
        DEPLOYMENT_YAML_PATH = 'deployment.yml'
    }
    
    stages {
        stage('Login to OpenShift') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'openshift-service-account-token', variable: 'OPENSHIFT_TOKEN')]) {
                        sh 'oc login --token=$OPENSHIFT_TOKEN --server=$OPENSHIFT_SERVER'
                    }
                }
            }
        }
        
        stage('Clone Git Repository') {
            steps {
                script {
                    git branch: 'main', url: GIT_REPO_URL
                }
            }
        }
        
        stage('Deploy to OpenShift') {
            steps {
                script {
                    sh "oc apply -f ${DEPLOYMENT_YAML_PATH} -n ${OPENSHIFT_NAMESPACE}"
                }
            }
        }
    }
}
