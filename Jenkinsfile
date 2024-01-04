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
    }
}