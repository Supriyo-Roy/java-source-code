pipeline{
    agent any
    stages{
        stage('Testing'){
            steps{
                git 'https://github.com/Supriyo-Roy/java-source-code.git'
                sh 'mvn test'
            }
        }
        stage("Building"){
            steps{
             git 'https://github.com/Supriyo-Roy/java-source-code.git'
             sh 'mvn install'
             archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage("Deploy on Test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-ec2-cred', path: '', url: 'http://15.206.195.45:8080/')], contextPath: '/app', war: '**/*.war'
            }
        }
        stage("Deploy on Prod"){
            steps{
                input 'Proceed with deployment on Prod server'
                deploy adapters: [tomcat9(credentialsId: 'tomcat-ec2-cred', path: '', url: 'http://65.0.71.209:8080/')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
}
