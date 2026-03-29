pipeline {
    agent none
    stages {
        stage('Build') {
            agent any
            steps {
                sh 'echo "This line is build in building stage" > file.txt'
                //stash → save file inside Jenkins
                //Stash is temporary (only for that pipeline run). Not for large files.
                //For big artifacts → use: S3, Nexus, Artifactory
                stash name: 'myfile', includes: 'file.txt'
            }
        }
        stage('Test') {
            agent { label 'node1'}
            steps {
                echo 'Testing if file exists'
                script { if (fileExists('file.txt')){        // This is script in groovy
                    sh 'rm -f file.txt' } }                 // Due to -f it will find b4 deleting and not throw error
                sh 'ls -l file.txt || echo "failed"'
                //unstash → restore file in another stage
                unstash 'myfile'
                //It will not fail bcoz of unstash as it will paste the file
                sh 'test -f file.txt'
                sleep 4
            }
        }
        stage('Deploy') {
            agent any
            steps {
                sh 'cat file.txt'
            }
        }

    }
}
