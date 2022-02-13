pipeline {
    agent any 
    stages {
        stage('Iac wordpress') { 
            steps {
                sh 'id'
                sh 'cd /home/vagrant/test_inv ; terraform apply -auto-approve'
                sh 'IPADD=$(az vm show -d -g resorses -n test_wordpress  --query publicIps -o tsv); printf "[test_deploy]\n$IPADD" > /home/vagrant/ansible/host.txt'
            }
        }
       
        stage('copy wordpress') { 
            steps {
                
                 
                //sh 'IPADD=$(az vm show -d -g res -n mysql  --query publicIps -o tsv); printf "[mysql]\n$IPADD" > /home/vagrant/ansible/host'
                sleep(time: 1, unit: "SECONDS")
                sh 'ls'
            }
        }
        
        
        stage('ansible wordpress') { 
            steps {
                  sh 'id'
                  sh 'cat /home/vagrant/ansible/host.txt'
                  sh 'ansible-playbook /home/vagrant/ansible/test_deploy.yml -i /home/vagrant/ansible/host.txt -b' 
                //sh 'cat /home/vagrant/ansible/host.txt'
                //sh 'rm /home/vagrant/ansible/host.txt'
                
            }
        }
        
        stage('copy wordpress') { 
            steps {
                //sh 'git clone https://github.com/Dmytrovel/wordpress.git'
                 sh 'scp -i /home/vagrant/azure_rsa  -r /var/lib/jenkins/workspace/j/  azureuser@20.113.24.4:/var/www/html/'
                //sh 'cat /home/vagrant/ansible/host.txt'
                //sh 'ansible-playbook /home/vagrant/ansible/mysql.yml -i /home/vagrant/ansible/host -b' 
                //sh 'cat /home/vagrant/ansible/host'
                //sh 'rm /home/vagrant/ansible/host'
                
            }
        }
    }
}
