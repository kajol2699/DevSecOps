pipeline {
    agent any
    
    tools{
        jdk 'jdk17'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git changelog: false, poll: false, url: 'https://github.com/shubnimkar/CI_CD_Devsecops.git'
            }
        }

        stage ('Check secrets') {
          steps {
              sh 'trufflehog3 https://github.com/shubnimkar/CI_CD_Devsecops.git -f html -o truffelhog_report.html || true'
              
      }
            post {
        always {
            // Publish the Trufflehog HTML report using the "Publish HTML reports" plugin
            publishHTML(target: [
                allowMissing: true,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: '',
                reportFiles: 'truffelhog_report.html',
                reportName: 'Trufflehog Scan Report'
            ])
        }
    }
        
    }
}
}
