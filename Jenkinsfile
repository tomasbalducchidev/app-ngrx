pipeline {
    agent any

    // environment {
    //     // Define Node.js path if necessary
    //     NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
    //     PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    // }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/your-repo.git', branch: 'main'
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
        }

        stage('Build Angular App') {
            steps {
                sh 'ng build --prod'
            }
        }

        stage('Deploy') {
            steps {
                // Ejemplo: Copiar archivos a un servidor web (Nginx o S3)
                sh 'scp -r dist/your-angular-app/ user@your-deployment-server:/var/www/html/'
            }
        }
    }

    post {
        always {
            // Publicar resultados de tests
            junit 'test-results/test-results.xml'
        }
    }
}
