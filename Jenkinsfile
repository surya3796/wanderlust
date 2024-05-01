pipeline{
    agent any
    environment{
        SCANNER_HOME = tool "sonar-scanner"
    }
    
    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'master', url: 'https://github.com/surya3796/wanderlust.git'
            }
        }
        stage("SonarQube Analysis"){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh "$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Wanderlust -DprojectName=Wanderlust"
                    
                }
            }
        }
        
        stage("Quality Gate"){
            steps{
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
            }
        }
        
        stage("OWASP Dependency Check"){
            steps{
                dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'dependency-check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage("File System Scan"){
            steps{
                sh 'trivy fs --format table -o trivy-fs-report.html .'
            }
        }
        stage("Deploy using Docker Compose"){
            steps{
                sh 'docker compose up -d'
            }
        }
    }
}
