pipeline {
    agent any
    environment {
        NEXUS_USER         = credentials('nexus-user')
        NEXUS_PASSWORD     = credentials('nexus-pass')
    }
    parameters {
        choice choices: ['Maven', 'Gradle'], description: 'Seleccione una herramienta para proceder a compilar', name: 'compileTool'
    }
    stages {
        stage("Pipeline"){
            steps {
                script{
                  switch(params.compileTool)
                    {
                        case 'Maven':
                            def ejecucion = load 'maven.groovy'
                            ejecucion.call()
                        break;
                        case 'Gradle':
                            def ejecucion = load 'gradle.groovy'
                            ejecucion.call()
                        break;
                    }
                }
            }
        }
    }
    post {
        always {
            sh "echo 'fase always executed post'"
        }
        success {
            sh "echo 'fase success'"
        }
        failure {
            sh "echo 'fase failure'"
        }
    }
}