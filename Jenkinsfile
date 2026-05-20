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
            sh """
                curl -H "Content-Type: application/json" \
                -X POST \
                -d '{"content": "✅ Pipeline EXITOSO - Build #${BUILD_NUMBER}"}' \
                https://discord.com/api/webhooks/1506780330231595110/_ck6OBwlOnHPFaPyED-xhpCO4z1m-4THYJa1FuJ-3Soom0_IJYjcH6ZcZEao2Jzj_SzR
            """
        }
        failure {
            mail to: 'masquebugs1@gmail.com',
            subject: 'Pipeline FALLÓ',
            body: 'La compilación o pruebas presentaron errores.'
            sh """
                curl -H "Content-Type: application/json" \
                -X POST \
                -d '{"content": "❌ Pipeline FALLÓ - Build #${BUILD_NUMBER}"}' \
                https://discord.com/api/webhooks/1506780330231595110/_ck6OBwlOnHPFaPyED-xhpCO4z1m-4THYJa1FuJ-3Soom0_IJYjcH6ZcZEao2Jzj_SzR
            """
        }
    }
}