pipeline {
    agent any
    tools {
        maven "maven3.8.1"
        jdk "jdk16"
    }
    stages {
        stage("Env Variables") {
            steps {
                sh "printenv"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Sonar'){
        	steps {
        		sh 'mvn verify sonar:sonar -Dsonar.projectKey=javigon258_m3-01-maven-clase -Dsonar.organization=javigon258 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=b474eb80d4c50bb5e94216e82c70e26f3ed85206 -Dsonar.branch.name=master'
        	}
        }
    }
}
