pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm 
            }
        }
   //# agent {
    //#    docker {
    //#        image 'maven:3-alpine'
    //#        args '-v /root/.m2:/root/.m2'
    //#    }
    
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('deploy') {
            steps {
                bat 'mvn cargo:deploy'
            }
        }
    }
}




