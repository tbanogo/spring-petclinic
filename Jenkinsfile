pipeline {
    agent any 
    
    
    stages {
        
        stage('Package') {
            steps {
                sh './mvnw package'
            }
        }
        
        
        stage('Capture') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                
                jacoco()
                junit '**/target/surefire-reports/*xml'
            
                emailext body: 'Ceci est un test', recipientProviders: [requestor(), culprits()], subject: 'Pipeline', to: 'testeur@stulink.org'
            }
        }
    }
    
    
    post {
        success {
            echo 'Build succeeded!'
        }
        
        
        failure {
            echo 'Build failed!'
        }
    }
}




