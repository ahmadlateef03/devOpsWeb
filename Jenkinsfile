pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
                steps {
                       deploy adapters: [tomcat7(credentialsId: 'tomcat_manager-gui', path: '', url: 'http://13.232.110.90:8081/')], contextPath: null, war: '**/*.war'
                    }
                }
    }
}
