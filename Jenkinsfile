pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'EXECUTE_TESTS', defaultValue: true, description: '')
        booleanParam(name: 'RUN_SONAR_SCAN', defaultValue: true, description: '')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'stg', 'prod'], description: 'Environment where the code should be deployed')
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: '')
        booleanParam(name: 'RUN_MIGRATION', defaultValue: true, description: '')
    }
    
    stages {
        stage("Build") {
            steps {
                sh 'export PATH=/usr/local/share/dotnet:$PATH'
                echo "Build the application"
                echo "Branch is ${env.BRANCH_NAME}"
                sh 'dotnet build'
            }
        }
        
        stage('Test') {
            when {
                expression {
                    params.EXECUTE_TESTS
                }
            }
            steps {
                echo 'Test'
//                 dotnetTest project: 'CareerPath.sln', sdk: '.NET Linux SDK 6.0', logger: 'trx;logFileName=TestResult.trx', collect: 'XPlat Code Coverage'
//                 mstest testResultsFile:"**/TestResult.trx", keepLongStdio: true
            }
        }
        
        stage("Deploy") {
            steps {
                echo "Deploy the application"
            }
        }
    }
}