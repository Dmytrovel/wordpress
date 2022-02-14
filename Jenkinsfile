pipeline {
    agent any 
    stages {
         stage('testing') { 
            steps {
                  //sh 'curl --header 'Content-Type: application/json' --request 'POST' --data '{"chat_id":"470290455","text":"build finished"}' "https://api.telegram.org/bot5279835931:AAFAjn7c6z6KCcb1U_zkVxkpSMVqGkNIH2Y/sendMessage"'
                  sh 'ansible-playbook /home/vagrant/ansible/errortest.yml -i /home/vagrant/ansible/host1.txt -b'
                 
           }
        }
        
        stage('terraform wordpress') { 
            steps {
                sh 'cd /home/vagrant/test_inv ; terraform apply -auto-approve'
                sh 'IPADD=$(az vm show -d -g resorses -n test_wordpress  --query publicIps -o tsv); printf "[test_deploy]\n$IPADD" > /home/vagrant/ansible/host.txt'
            }
        }
        stage('ansible') { 
            steps {
                  sh 'cat /home/vagrant/ansible/host.txt'
                  sh 'ansible-playbook /home/vagrant/ansible/test_deploy.yml -i /home/vagrant/ansible/host.txt -b' 
            }
        }
        stage('copy wordpress') { 
            steps {
                  sh 'curl --header 'Content-Type: application/json' --request 'POST' --data '{"chat_id":"470290455","text":"build finished"}' "https://api.telegram.org/bot5279835931:AAFAjn7c6z6KCcb1U_zkVxkpSMVqGkNIH2Y/sendMessage"'
                  //sh 'IPADD2=$(az vm show -d -g resorses -n test_wordpress  --query publicIps -o tsv); scp -i /home/vagrant/azure_rsa  -r /var/lib/jenkins/workspace/j/  azureuser@$IPADD2:/var/www/html/'
            }
        }
    }
}
