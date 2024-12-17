pipeline {
    agent any

    stages {
        stage('Copy Playbook') {
            steps {
                script {
                    echo 'Copying Ansible playbook to remote server...'
                    sh '''
                    ls -l /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml
                    scp -i /var/lib/jenkins/.ssh/id_rsa_jenkins \
                    /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml \
                    root@99.79.79.222:/tmp/playbook-nginx.yml
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Executing Build Stage on remote server...'
                    sh '''
                    ansible-playbook -i /tmp/inventory/hosts \
                    /tmp/playbook-nginx.yml \
                    -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Executing Test Stage...'
                    sh '''
                    ansible-playbook -i /tmp/inventory/hosts \
                    /tmp/playbook-nginx.yml --tags save \
                    -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline executed successfully.'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
pipeline {
    agent any

    stages {
        stage('Copy Playbook') {
            steps {
                sh '''
                scp -i /var/lib/jenkins/.ssh/id_rsa_jenkins \
                /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml \
                root@99.79.79.222:/tmp/playbook-nginx.yml
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                ansible-playbook -i /tmp/inventory/hosts \
                /tmp/playbook-nginx.yml \
                -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins
                '''
            }
        }
    }
}
