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
                withCredentials([usernamePassword(credentialsId: 'worker-sudo-pass', usernameVariable: 'SUDO_USER', passwordVariable: 'SUDO_PASS')]){
                    sh "ansible-playbook -i inventory.ini docker_pull.yml -e 'ansible_become_password=${SUDO_PASS}'"
                }
            }
        }

        stage("Deploy"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'worker-sudo-pass', usernameVariable: 'SUDO_USER', passwordVariable: 'SUDO_PASS')]){
                    sh "ansible-playbook -i inventory.ini docker_deploy.yml -e 'ansible_become_password=${SUDO_PASS}'"
                }
            }
        }
    }
}