pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "This line is build in building stage" > file.txt'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing if file exists'
                sh 'ls -l file.txt'
                sh 'test -f file.txt'
                sleep 4
            }
        }
        stage('Deploy') {
            steps {
                sh 'cat file.txt'
            }
        }

    }
}
