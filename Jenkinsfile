pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    parameters {
        choice(name:'VERSION', choices:['1.0', '1.1', '1.2'], description:'Choose the version of the project')

        booleanParam(name :'executeTests', description:'Execute the tests', defaultValue:false)
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                // sh 'npm run test'
                echo 'run tests here'
            }
        }
        stage('Build Image') {
            steps {
                sh 'npm run  build'
            
            }
        }
        stage ('Deploy') {
            steps {
                echo 'Deploying the application'
                
            }
        }
    }
}                                                                                                                                                                                                        