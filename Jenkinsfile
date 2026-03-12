node {

}

stage('Build') {
    docker.image('composer:latest').inside('-u root') {
        sh 'rm -f composer.lock'
        sh 'composer install'
    }
}

stage('Testing') {
    docker.image('ubuntu').inside('-u root') {
        sh 'echo "Ini adalah test pipeline Jenkins"'
    }
}

// deploy env prod
stage('Deploy') {
    docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
        sshagent (credentials: ['ssh-prod']) {

            sh 'mkdir -p ~/.ssh'

            sh 'ssh-keyscan -H "$PROD_HOST" >> ~/.ssh/known_hosts || true'

            sh 'rsync -rav --delete ./ adms26@$PROD_HOST:/home/adms26/ansible-deploy/prod.kelasdevops.xyz/ --exclude=.env --exclude=storage --exclude=.git'
        }
    }
}