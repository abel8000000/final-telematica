  pipeline {
      agent any
      stages {
          stage('Deploy to EC2') {
              steps {
                  sshagent(['ec2-ssh-key']) {
                      sh '''
                          set -x
                          scp -o StrictHostKeyChecking=no scripts/deploy.sh ubuntu@44.211.161.180:~/deploy.sh
                          ssh -o StrictHostKeyChecking=no ubuntu@44.211.161.180 << 'ENDSSH'
                              source ~/.bash_profile
                              export PATH=$PATH:/usr/local/bin:/usr/bin
                              echo "Cleaning up old application directory..."
                              rm -rf ~/app
                              echo "Cloning the repository..."
                              git clone https://github.com/abel8000000/final-telematica.git ~/app
                              cd ~/app/scripts
                              chmod +x deploy.sh
                              ./deploy.sh
                          ENDSSH
                      '''
                  }
              }
          }
      }
  }
