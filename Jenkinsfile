pipeline {
    agent { label 'master' }
    options {
        buildDiscarder(logRotator(numToKeepStr: '20'))
        timestamps()
    }

 stages {
        stage ('Checkout') {
            agent {
                node {
                      label 'ansible-tomcat-nodes'
                      customWorkspace "ansible-tomcat"
                     }
            }
            steps {
                script {
                     checkout scm
                }
            }
       }    
     
        stage ('InstallTomcat') {
            agent {
                node {
                      label 'ansible-tomcat-nodes'
                      customWorkspace "ansible-tomcat"
                      }
  }
           
            steps {
                   ansiblePlaybook(
                   credentialsId: 'ansible-tomcat-nodes-ssh-key',
                   inventory: 'hosts',
                   playbook: 'multiple-tomcat-setup.yml',                  
                   hostKeyChecking: false,
                   )
}      
    }
  }
}
