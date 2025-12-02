pipeline {          
    agent any         
    
    stages {  
        stage('Git Checkout') {
            steps {
                git branch: 'golang', credentialsId: 'ssh_global_sep15_v_ID', url: 'git@github.com:agilitydelivered/ad-jenkins-qa-python.git' 
               //  git branch: 'golang', credentialsId: 'ssh_prod_global_v_oct10_ID', url: 'git@github.com:agilitydelivered/ad-jenkins-qa-python.git' 

                
            }
        }
        
        stage('Build') {
            steps {
                sh '''
                    sudo apt-get update -y || sudo apt-get update --fix-missing -y
                    sudo apt-get install -y golang-go
                    go version
                    cd hello
                    go mod tidy
                    go build                                       
                '''
                
            }
        }
    }
    
    post {
        always {
            script {
                emailext(
                    subject: "pipeline-script-build",
                    body: '${JELLY_SCRIPT, template="ad_default_template"}',
                    mimeType: 'text/html',
                    to: 'jeya.veronica@agilitydelivered.com',
                )
            }
        }
    }
}
