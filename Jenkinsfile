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
        parallel {
                stage('Unit Tests & Code Coverage') {
                    agent {
                        label "for-branch-a"
                    }
                    steps {
                        sh 'mvn test'
                
                        publishHTML target: [
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'coverage',
                            reportFiles: 'index.html',
                            reportName: 'RCov Report'
                        ]
                    }
                }
                stage('Sonarcube') {
                    agent {
                        label "for-branch-b"
                    }
                    steps {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=back-endd -Dsonar.organization=kcelestine-github -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=3c1a0d7728eb2d4de7b4684e8d18293ebd7ef91e' 
                    }
                }
        }
  
        
        stage ('Deploy to Dev') {
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
