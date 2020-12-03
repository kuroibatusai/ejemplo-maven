pipeline {
    agent any

    stages {
        stage('Compilar') {
            steps {
                    sh './mvnw clean compile -e'
            }
        }
        stage('Test') {
            steps {
                    sh './mvnw clean test -e'
            }
        }
        stage('JarCode') {
            steps {
                    sh './mvnw clean package -e'
            }
        }
        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonar') //Nombre del SonarQube Server de Configurar Sistema en Jenkins 
                { // You can override the credential to be used
                    sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }
        }
        stage('RunJar') {
            steps {
                    sh 'nohup bash mvnw spring-boot:run &'
                    sh 'sleep 20'
            }
        }
        stage('Curl') {
            steps {
                    sh 'sleep 60'
                    sh 'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing" '
            }
        }
    }
}
