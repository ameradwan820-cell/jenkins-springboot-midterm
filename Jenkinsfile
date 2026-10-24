pipeline {
    agent any

    stages {
        stage('Check Tools') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Build Fat JAR') {
            steps {
                sh 'mvn -B clean package'
            }
        }

        stage('Verify Fat JAR') {
            steps {
                sh '''
                    test -s target/amer-midterm.jar
                    jar tf target/amer-midterm.jar > target/jar-contents.txt
                    grep 'BOOT-INF/lib/' target/jar-contents.txt
                    ls -lh target/amer-midterm.jar
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/amer-midterm.jar',
                                 fingerprint: true
            }
        }
    }
}
