pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/tomasbalducchidev/app-ngrx.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'rm -rf node_modules package-lock.json'
                    sh 'node --max_old_space_size=4096 $(which npm) install'
                    sh 'npm install --no-cache'
                }
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test -- --watch=false --browsers=ChromeHeadless'
            }
            post {
              always {
                junit 'test-results/test-results.xml'
            }
        }
        }

        stage('Build Angular App') {
            steps {
                sh 'ng build --prod'
            }
        }

        stage('Deploy') {
            steps {
                sh 'scp -r dist/app-ngrx/ ubuntu@ip-172-31-28-46:/var/www/html/'
            }
        }
    }


}
