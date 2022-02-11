node{
    stage('Clone') {
        checkout scm
    }

    stage('Init') {
        sh "apk add ansible sshpass"
        sh "rm -rf /root/.ssh"
        sh "echo '192.168.158.131 app-salaire.jarod.form' > /etc/hosts"
        sh "ssh-keygen -q -t rsa -N '' -f ~/.ssh/id_rsa"
        sh "sshpass -p 'jarjar' ssh-copy-id -o stricthostkeychecking=no root@app-salaire.jarod.form"
    }

    stage('Ansible') {
      ansiblePlaybook (
          colorized: true,          
          playbook: 'playbook.yml',
          inventory: 'hosts.yml'
      )
    }
}
