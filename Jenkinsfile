node {
     
  stage('Git-Checkout') {
   sh 'rm -rf debit_card_management_app'
   sh 'git clone -b master https://devops311@bitbucket.org/accelerators-devops/debit_card_management_app.git'
  }
    
 def project_path="ansible"
 
 dir(project_path) {
 stage(' Downloading Jar From Artifactory Locally'){
    def server= Artifactory.server 'Artifactory'
    def downloadSpec = """{
    "files": [
    {
      "pattern": "debit-card-application-test/*.war",
      "target": "/var/lib/jenkins/workspace/production-deployment-role/war-storage-prod/"
      
    }
    ]
    }"""
    server.download(downloadSpec)
   
}
stage('Ansible Playbook Execution') {
sh label: 'Ansible', script: 'ansible-playbook -i inventory -u prod playbook.yml'
}
}
}