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
        sshagent(['ssh-prod']) {
            sh '''
            mkdir -p ~/.ssh
            ssh-keyscan -H prod.kelasdevops.xyz >> ~/.ssh/known_hosts

            rsync -rav --delete ./ ajiiee@prod.kelasdevops.xyz:/home/ajiiee/ansible-deploy/prod.kelasdevops.xyz/ \
            --exclude=.env --exclude=storage --exclude=.git
            '''
        }
    }
}
    }
}