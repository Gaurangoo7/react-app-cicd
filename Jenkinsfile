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
                    sh 'docker build -t gaurang1/sample-react-app .'
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push gaurang1/sample-react-app'
                }
            }
        }
        stage ('Deploy') {
            steps {
                script {
                    def dockerCmd = 'docker run  -p 3000:3000 -d gaurang1/sample-react-app:latest'
                    sshagent(['15276518-eb21-4181-93eb-64e8d78f45d0']) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@34.201.101.177 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
