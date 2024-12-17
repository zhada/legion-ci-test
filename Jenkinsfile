pipeline {
    agent any

    stages {
        stage('Copy Playbook') {
            steps {
                script {
                    echo 'Copying Ansible playbook to the remote server...'
                    sh '''
                    scp -i /var/lib/jenkins/.ssh/id_rsa_jenkins \
                    /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml \
                    root@99.79.79.222:/root/playbook-nginx.yml
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Executing Build Stage on remote server...'
                    sh '''
                    ansible-playbook -i /var/lib/jenkins/src/legion-ci-test/hosts \
                    /root/playbook-nginx.yml \
                    -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Executing Test Stage on remote server...'
                    sh '''
                    ansible-playbook -i /var/lib/jenkins/src/legion-ci-test/hosts \
                    /root/playbook-nginx.yml --tags save \
                    -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins
                    '''
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Pipeline execution complete.'
            }
        }
        success {
            script {
                echo 'Pipeline executed successfully.'
            }
        }
        failure {
            script {
                echo 'Pipeline failed. Check logs for details.'
            }
        }
    }
}
