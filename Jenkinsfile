pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shikharadhikari/portfolio-template-demo.git'
            }
        }

        stage('Validate') {
            steps {
                sh '''
                    set -eu
                    test -f index.html
                    test -f style.css
                    test -f script.js
                '''
            }
        }

        stage('Deploy Portfolio') {
    steps {
        sh '''
            set -eu

            rsync -rv --delete \
                --no-perms \
                --no-owner \
                --no-group \
                --omit-dir-times \
                --exclude='.git/' \
                --exclude='Jenkinsfile' \
                ./ /var/www/website-one/
        '''
    }
}

        stage('Verify') {
            steps {
                sh 'test -s /var/www/website-one/index.html'
                sh 'curl -fsS http://localhost:8081/ > /dev/null'
            }
        }
    }
}
