pipeline {
    agent any

    environment {
        // Define la URL del ambiente como variable de entorno
        TEST_ENV_URL = 'https://fakeapi.net' // Puedes cambiar esto desde Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Clona el repositorio desde GitHub
                git branch: 'main', url: 'https://github.com/jm84/jmeterjenkinsTest.git'
            }
        }

        stage('Run JMeter Test') {
            steps {
                // Ejecuta el test plan de JMeter
                script {
                    sh """
                    jmeter -n -t test-plan.jmx -JURL=${TEST_ENV_URL} -l results.jtl
                    """
                }
            }
        }

        stage('Publish Results') {
            steps {
                // Publica los resultados usando el Performance Plugin
                perfReport parsers: [[$class: 'JUnitParser', glob: 'results.jtl']]
            }
        }
    }
}