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

        stage('Install Dependenciesss') {
    steps {
        script {
            timeout(time: 10, unit: 'MINUTES') {
                sh 'npm ci'
            }
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
