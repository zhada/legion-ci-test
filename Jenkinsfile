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
