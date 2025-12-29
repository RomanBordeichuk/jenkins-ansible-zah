pipeline{
    agent any

    environment{
        ANSIBLE_HOST_KEY_CHECKING = false
    }

    stages{
        stage("Pull image from DockerHub"){
            steps{
                sh "ansible-playbook -i inventory.ini docker_pull.yml"
            }
        }

        stage("Deploy"){
            steps{
                sh "ansible-playbook -i inventory.ini docker_deploy.yml"
            }
        }
    }
}