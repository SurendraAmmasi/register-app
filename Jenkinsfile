pipeline {
    agent{ label 'Jenkins-Agent' }
    tools{
        maven 'Maven3'
        jdk 'Java17'
    }

    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }

        stage( "Checkout from SCM" ){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/SurendraAmmasi/register-app.git'
            }
        }

        stage( "Build Application" ){
            steps{
                sh "mvn clean package"
            }
        }

        stage( "Test Application" ){
            steps{
                sh "mvn test"
            }
        }

        stage( "SonarQube Analysis" ){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token'){
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }

        stage( "Quality Gate" ){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube-token'
                }
            }
        }
    }
}