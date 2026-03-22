pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "This line is build in building stage" > file.txt'
                stash name: 'myfile', includes: 'file.txt'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing if file exists'
                sh 'rm file.txt'
                sh 'ls -l file.txt || failed'
                echo 'Unstashing to paste the stashed file'
                unstash 'myfile'
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
