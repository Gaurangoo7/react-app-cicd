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
                // sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                // sh 'npm run test'
                echo "Test"

            }
        }
        stage('Build Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: '1ec90535-d958-4a41-aa96-8719bd392206', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh 'docker build -t gaurang1/sample-react-app-1 .'
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push gaurang1/sample-react-app-1'
                }
            }
        }
        stage ('Deploy') {
            steps {
                sh 'docker run -d -i -t --name react-container-app -p 3000:3000 sample-react-app:latest'
            }
        }
    }
}
