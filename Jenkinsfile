pipeline {
    agent { label 'jenkins-node' }  // Execute the pipeline on 'jenkins-node'

    stages {
        stage('Build') {
            steps {
                echo 'Executing Build Stage on jenkins-node...'
                sh '''
                ansible-playbook \
                -i /var/lib/jenkins/src/legion-ci-test/inventory/hosts \
                /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml \
                -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Executing Test Stage on jenkins-node...'
                sh '''
                ansible-playbook \
                -i /var/lib/jenkins/src/legion-ci-test/inventory/hosts \
                /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml \
                --tags save -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins
                '''
            }
        }
    }
}
