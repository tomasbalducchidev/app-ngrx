pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

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
                sh 'npm install'
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
