pipeline{

    agent any

    stages{

        stage('Continous Download') {

            steps{
                git branch: 'main', url: 'https://github.com/Hadijah-ateh/My-Pipeline.git'
            }
        }
        stage("Intergration Testing"){

            steps{
                sh 'mvn verify -DskipUnitTest'
            }
        }
        stage("Unit Testing"){

            steps{
                sh 'mvn test'
            }
        }
        stage("Contious Biuld"){

            steps{
                sh 'mvn clean install'
            }
        }
        stage("Static Test Analysis"){

            steps{

                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube-token'){
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("Quality Gate Analysis"){

            steps{

                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-token'
                }
            }
        }
        stage("Upload Artifact To Nexus"){

            steps{

                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: '', groupId: 'com.example', nexusUrl: '35.91.94.40:8081', nexusVersion: 'nexus2', protocol: 'http', repository: 'Devops-project', version: '1.0.1'
                }
            }
        }
    }
}