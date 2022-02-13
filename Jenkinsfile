pipeline {
    agent any 
    stages {
        stage('terraform wordpress') { 
            steps {
                sh 'id'
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
        stage('copy wordpress1') { 
            steps {
                  sh 'scp -i /home/vagrant/azure_rsa  -r /var/lib/jenkins/workspace/j/  azureuser@$IPADD:/var/www/html/'
            }
        }
    }
}
