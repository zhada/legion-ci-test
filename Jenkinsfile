pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'ansible-playbook -i /var/lib/jenkins/src/legion-ci-test/inventory/hosts  /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins'

            }
        }

        stage('Test') {
            steps {
                sh 'ansible-playbook -i /var/lib/jenkins/src/legion-ci-test/inventory/hosts /var/lib/jenkins/src/legion-ci-test/playbook-nginx.yml --tags save -u root --private-key /var/lib/jenkins/.ssh/id_rsa_jenkins'

    
            }
        }
    }
}
