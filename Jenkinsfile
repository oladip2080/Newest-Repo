pipeline {
    agent any

    stages {
        stage('Git Checkout?') {
            steps {
                git 'https://github.com/oladip2080/Newest-Repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'cd MyWebApp && mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'cd MyWebApp mvn test'
            }
        }
        stage {'Code Quality scan'} {
            steps{
                withSonarQubeEnv{'sonar'} {
                    sh "mvn -f MyWebApp/pom.xml sonar:sonar"
                }
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.14.68.147:8080/')], contextPath: 'path', war: '**/*.war'
            }
        }
    }
}
