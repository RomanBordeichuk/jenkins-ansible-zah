pipeline{
    agent any

    environment{
        ANSIBLE_HOST_KEY_CHECKING = false
    }

    stages{
        stage("Debug Info") {
            steps {
                sh "whoami"
                sh "pwd"
                sh "ls -la ~/.ssh/"
            }
        }

        stage("Pull image from DockerHub"){
            steps{
                withCredentials([string(credentialsId: 'worder-sudo-pass', variable: 'SUDO_PASS')]){
                    sh "ansible-playbook -i inventory.ini docker_pull.yml -e 'ansible_become_password=${SUDO_PASS}'"
                }
            }
        }

        stage("Deploy"){
            steps{
                withCredentials([string(credentialsId: 'worder-sudo-pass', variable: 'SUDO_PASS')]){
                    sh "ansible-playbook -i inventory.ini docker_deploy.yml -e 'ansible_become_password=${SUDO_PASS}'"
                }
            }
        }
    }
}