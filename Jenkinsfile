pipeline {
    agent any

    stages {
        stage('Compilar') {
            steps {
                dir('/Users/kuroi/Desktop/DiplomadoDevOps/ejemplo-maven'){
                    sh './mvnw clean compile -e'
                }
            }
        }
        stage('Test') {
            steps {
                dir('/Users/kuroi/Desktop/DiplomadoDevOps/ejemplo-maven'){
                    sh './mvnw clean test -e'
                }
            }
        }
        stage('JarCode') {
            steps {
                dir('/Users/kuroi/Desktop/DiplomadoDevOps/ejemplo-maven'){
                    sh './mvnw clean package -e'
                }
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
                dir('/Users/kuroi/Desktop/DiplomadoDevOps/ejemplo-maven'){
                    sh 'nohup bash mvnw spring-boot:run &'
                    sh 'sleep 20'
                }
            }
        }
        stage('Curl') {
            steps {
                dir('/Users/kuroi/Desktop/DiplomadoDevOps/ejemplo-maven'){
                    sh 'sleep 60'
                    sh 'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing" '
                }
            }
        }
    }
}
