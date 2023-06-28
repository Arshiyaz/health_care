node{
    stage('code_checkout')
    {
        git branch: 'master', url: 'https://github.com/Arshiyaz/health_care.git'
    }

    stage('code_build'){
    
    sh 'mvn clean package'
    }
    stage('docker_image_build')
    {
    sh 'sudo docker build -t arshiya13/healthcare .'
   
    }
    stage('docker image push')
    {
    
    withCredentials([string(credentialsId: 'dockerid', variable: 'dockervar')]) {
        sh 'docker login -u arshiya13 -p ${dockervar}'
        sh 'docker push arshiya13/healthcare'
    
}
    }
    stage('ansible_deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansibleid', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
