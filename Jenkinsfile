pipeline {
    agent {
        label 'Ansible-Agent'
    }
    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main' ,
                   url: 'https://github.com/Ani-Jenkins/Jenkins-Ansible.git'
            }
        }
        stage('Verify Ansible Installation') {
            steps {
                sh 'whereis ansible-playbook'
                sh 'whereis ansible-lint'
            }
        }
        stage('Verify Playbook Quality') {
            steps{
                sh 'ansible-playbook jenkins.yml --syntax-check -i inventory2'
                sh 'ansible-lint jenkins.yml'
            }
                
        }
        stage('Run Ansible Playbook') {
            steps {
                sh 'ansible-playbook jenkins.yml -i inventory2'
            }
        }
    }
    post{
        always {
            archiveArtifacts '*.log'
        }
        success {
            echo "Ansible Playbook Executed Successfully"
        }
        failure {
            echo "Ansible Playbook Failed"
        }
    }
}
