pipeline {
    agent any
    
     parameters {
        string(name: 'TEST_ENV_URL', defaultValue: 'fakeapi.net', description: 'URL del ambiente para el test plan de JMeter')
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
                    bat """
                    jmeter -n -t testfakeapi.jmx -JURL=${TEST_ENV_URL} -l results.jtl
                    """
                }
            }
        }

        stage('Publish Results') {
            steps {
                // Publica los resultados usando el Performance Plugin
                perfReport sourceDataFiles: 'results.jtl'
            }
        }
    }
}