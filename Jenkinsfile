pipeline{
    agent any
    environment {
        BUILD_AUTOMATION_TOOL = "Jenkins"
        TEST_AUTOMATION_TOOL = "Katalon"
        CODE_ANALYSIS_TOOL = "PMD"
        SECURITY_SCAN_TOOL = "SpectralOps"
        STAGING_SERVER = "AWS EC2"
        PRODUCTION_SERVER = "AWS EC2"
        BUILD_LOG = "C:/Users/theex/.jenkins/jobs/6.2C/builds/40/log"
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
            success{
                mail to: "vittrutruggs@gmail.com",
                subject: "Security Scan Successful",
                body: "${BUILD_LOG, maxLines=1000, escapeHtml=false}"
                }
            failure{
                mail to: "vittrutruggs@gmail.com",
                subject: "Security Scan Unsuccessful",
                body: "${BUILD_LOG, maxLines=1000, escapeHtml=false}"
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
                mail to: "vittrutruggs@gmail.com",
                subject: "Integration Test Successful",
                body: "${BUILD_LOG, maxLines=1000, escapeHtml=false}"
                }
            failure{
                mail to: "vittrutruggs@gmail.com",
                subject: "Integration Test Unsuccessful",
                body: "${BUILD_LOG, maxLines=1000, escapeHtml=false}"
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
