pipeline{
    agent any

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