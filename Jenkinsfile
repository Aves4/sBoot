pipeline {

    agent any

    tools {
        jdk 'jdk8'          
        maven 'm360'
    }

    stages {

        stage('Debug Java') {
            steps {
                sh 'echo $JAVA_HOME'
                sh 'ls -l $JAVA_HOME/bin'
                sh 'java -version || true'
            }
        }

        stage('build') {
            steps {
                sh 'mvn install -DskipTests'
            }
        }

        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/**/*', followSymlinks: false
            junit stdioRetention: '', testResults: 'target/surefire-reports/*.xml'
        }
    }
}
