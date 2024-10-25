node{
    stage('checkout'){
        git 'https://github.com/akashbeni/Final-project.git'
    }
    
    stage('maven build'){
        sh 'mvn clean package'
    }
    
    stage('containerize'){
       // sh 'docker build -t akash028/insure-me:1.0 .'
    }
    stage('Release'){
      withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'dockerHubPwd')]) {
     // sh "docker login -u akash028 -p ${dockerHubPwd}"
      //sh 'docker push akash028/insure-me:1.0'
      }
    }
    stage('Deploy to Test'){
        ansiblePlaybook become: true, credentialsId: 'ansible-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml', vaultTmpPath: ''
        
    }
    stage('Selenium testing'){
        git 'https://github.com/akashbeni/DevopsFP-Selenium.git'
        
    }
    stage('Build'){
        sh 'mvn clean package assembly:single'
    }
    stage('Selenium Testing '){
        sh 'java -jar target/insureme-selenium-0.0.1-SNAPSHOT-jar-with-dependencies.jar'
    }
    stage('checkout'){
        git 'https://github.com/akashbeni/Final-project.git'
    }
    stage('maven build'){
        sh 'mvn clean package'
    }
    stage('Deploy to Prod'){
        ansiblePlaybook become: true, credentialsId: 'ansible-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-prod-server.yml', vaultTmpPath: ''
        
    }
    
}
