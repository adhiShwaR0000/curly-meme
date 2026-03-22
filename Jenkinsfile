pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "This line is build in building stage" > file.txt'
                //stash → save file inside Jenkins
                //Stash is temporary (only for that pipeline run). Not for large files.
                //For big artifacts → use: S3, Nexus, Artifactory
                stash name: 'myfile', includes: 'file.txt'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing if file exists'
                sh 'rm file.txt'
                sh 'ls -l file.txt || echo "failed"'
                echo 'Unstashing to paste the stashed file'
                //unstash → restore file in another stage
                unstash 'myfile'
                //It will not fail bcoz of unstash as it will paste the file
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
