pipeline {
    agent any
    tools { 
        maven 'Maven 3.3.9' 
        jdk 'jdk8' 
    }
    stages {
        stage('build') {
            steps {
                echo 'Khadijah'
                sh 'ls'
            }
        }
        
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
        
        stage ('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage ('Code Coverage') {
            steps {
                sh 'ls' 
            }
        }
        
        stage ('Sonarcube') {
            steps {
                sh 'ls' 
            }
        }   
        
        stage ('Deploy to Dev') {
            steps {
                sh 'ls' 
            }
        }  
        
        stage ('E2E Test') {
            steps {
                sh 'ls' 
            }
        }  
        
        stage ('Smoke Test') {
            steps {
                sh 'ls' 
            }
        }  
        
    } // end stages
    
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            junit 'target/surefire-reports/**/*.xml'
            archiveArtifacts artifacts: 'target/site/jacoco-both/index.html', fingerprint: true
        }
    }
}
