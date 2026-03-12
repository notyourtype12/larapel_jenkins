pipeline {
    agent any

    environment {
        DEPLOY_USER = 'ajiiee'
        DEPLOY_HOST = 'prod.kelasdevops.xyz'
        DEPLOY_PATH = '/home/ajiiee/ansible-deploy/prod.kelasdevops.xyz'
    }

    stages {
        stage('Deploy') {
            steps {
                sshagent(['SSH PROD']) {
                    sh '''
                    mkdir -p /root/.ssh
                    ssh-keyscan -H $DEPLOY_HOST >> /root/.ssh/known_hosts

                    rsync -rav --delete ./ $DEPLOY_USER@$DEPLOY_HOST:$DEPLOY_PATH \
                    --exclude=.env --exclude=storage --exclude=.git
                    '''
                }
            }
        }
    }
}