pipeline {
    agent any
    stages {
        stage('Build and Test') {
            steps {
                sh 'chmod +x mvnw && ./mvnw clean verify'
            }
        }
    }
    post {
        always {
            junit testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true
        }
        success {
            mail to: 'masquebugs1@gmail.com',
            subject: 'Pipeline EXITOSO',
            body: 'La compilación y pruebas finalizaron correctamente.'
        }
        failure {
            mail to: 'masquebugs1@gmail.com',
            subject: 'Pipeline FALLÓ',
            body: 'La compilación o pruebas presentaron errores.'
        }
    }
}