pipeline {
    agent{ label 'Jenkins-Agent' }
    tools{
        maven 'Maven 3'
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

        
    }
}