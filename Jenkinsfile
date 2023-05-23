pipeline{
    agent any
    environment {
        BUILD_AUTOMATION_TOOL = "Jenkins"
        TEST_AUTOMATION_TOOL = "Katalon"
        CODE_ANALYSIS_TOOL = "PMD"
        SECURITY_SCAN_TOOL = "SpectralOps"
        STAGING_SERVER = "AWS EC2"
        PRODUCTION_SERVER = "AWS EC2"
    }
    stages{
        stage('Build'){
            steps{
                echo "build, compile and pack code through: $BUILD_AUTOMATION_TOOL"
            }
        }
        stage('Unit and Integration Tests'){
            steps{
                echo "run unit tests and integration tests through: $TEST_AUTOMATION_TOOL"    
            }
        }
        stage('Code Analysis'){
            steps{
                echo "check the quality of the code through: $CODE_ANALYSIS_TOOL"    
            }
        }
        stage('Security Scan'){
            steps{
                echo "utilise: $SECURITY_SCAN_TOOL to perform security scan and identify vulnerabilities"
            }
        post{
           always {
                emailext attachLog:true, body: 'The security scan status is reported with the following logs', subject: 'Security Scan Status', to:'vittrutruggs@gmail.com'
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                echo "deploy the application to a testing environment specified by: $STAGING_SERVER"    
                }
        }
        stage('Integration Tests on Staging'){
            steps{
                echo "run integration tests on a staging environment specified by: $STAGING_SERVER"
            }
        post{
            success{
                emailext attachLog:true, body: 'The integration tests status is reported with the following logs', subject: 'Integration Tests Status', to:'vittrutruggs@gmail.com' 
                }
            }
        }
        stage('Deploy to Production'){
            steps{
                echo "Code deployed to production environment specified by: $PRODUCTION_SERVER"    
            }
        }  
    }
}
