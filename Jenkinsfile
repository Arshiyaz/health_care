node{
    stage('git checjout')
    {
        git branch: 'master', url: 'https://github.com/Arshiyaz/health_care.git'
    }

    stage('build'){
    
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t arshiya13/healthcare .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockerid', variable: 'dockervar')]) {
        sh 'docker login -u arshiya13 -p ${dockervar}'
        sh 'docker push arshiya13/healthcare'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansibleid', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
