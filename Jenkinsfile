pipeline {
    agent any
    
    parameters {
            choice(name: 'ENVIRONMENT', choices: ['dev', 'uat'], description: 'Selecciona el ambiente para la ejecución del test plan')
        }
    environment {
        TEST_ENV_URL = getEnvironmentUrl(params.ENVIRONMENT) // Asigna la URL según el ambiente seleccionado
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

// Función para asignar la URL según el ambiente seleccionado
def getEnvironmentUrl(environment) {
    switch (environment) {
        case 'dev':
            return 'fakeapi.net'
        case 'uat':
            return 'uat.example.com'
        default:
            error "Ambiente no válido: ${environment}"
    }
}