
pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Ansible Syntax Check') {
            steps {
                ansiblePlaybook(
                    playbook: 'facts.yaml',
                    credentialsId: 'ansible-ssh',
                    extras: '--syntax-check'
                )
            }
        }

        stage('Execute Ansible Playbook') {
            steps {
                ansiblePlaybook(
                    playbook: 'facts.yaml',
                    credentialsId: 'ansible-ssh',
                    extras: '-v'
                )
            }
        }
    }

    post {
        success {
            echo 'Configuration management completed successfully!'
        }

        failure {
            echo 'Ansible execution failed!'
        }
    }
}
