pipeline {
    agent any 
    tools{             
        maven 'maven-3.8'  
        }
    stages{
        stage('build jar') {
            steps {
                script {
                    echo "Building the application..."
                    sh 'mvn package'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "Building the dockerimage..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh 'docker build -t docker2624/pipeline .'
                        sh "docker login -u $USER -p $PASS"
                        sh 'docker push docker2624/pipeline'
                    }
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "deploying the application..."    
                }
            }        }
    }
}
