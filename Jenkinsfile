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
            success{
                    emailext attachLog: true,
                    body: "Security Scan Stage implemented successfully!" +
                            currentBuild.rawBuild.getLog(15).join("<br>"),

                    mimeType: 'text/html',
                    subject: "Security Scan Status",
                    to: '"vittrutruggs@gmail.com"'
                }
            failure{
                    emailext attachLog: true,
                    body: "Security Scan Stage implemented unsuccessfully!" +
                            currentBuild.rawBuild.getLog(15).join("<br>"),

                    mimeType: 'text/html',
                    subject: "Security Scan Status",
                    to: '"vittrutruggs@gmail.com"'
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
                emailext(
                    subject: "Security Scan Status",
                    to: "vittrutruggs@gmail.com",
                    body: """<p>Security Scan Stage implemented successfully!</p>
                    <p>Console output (last 250 lines):<hr><pre>${BUILD_LOG}</pre></p>"""                
                )
                }
            failure{
                emailext(
                    subject: "Security Scan Status",
                    to: "vittrutruggs@gmail.com",
                    body: """<p>Security Scan Stage implemented successfully!</p>
                    <p>Console output (last 250 lines):<hr><pre>${BUILD_LOG}</pre></p>"""                
                )
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
