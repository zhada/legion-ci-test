pipeline {
    agent { node 'jenkins-node' }

    stages {
        stage('Copy Playbook') {
            steps {
                // Copy playbook from Jenkins server to node
                sh '''
                scp -i /var/lib/jenkins/.ssh/id_rsa_jenkins \
                /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml \
                root@99.79.79.222:/tmp/playbook-nginx.yml
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Executing Build Stage on jenkins-node...'
                sh 'ansible-playbook -i /var/lib/jenkins/src/legion-ci-test/inventory/hosts /tmp/playbook-nginx.yml -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins'
            }
        }

        stage('Test') {
            steps {
                sh 'ansible-playbook -i /var/lib/jenkins/src/legion-ci-test/inventory/hosts /tmp/playbook-nginx.yml --tags save -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins'
            }
        }
    }
}
