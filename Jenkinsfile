pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'EXECUTE_TESTS', defaultValue: true, description: '')
        booleanParam(name: 'RUN_SONAR_SCAN', defaultValue: true, description: '')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'stg', 'prod'], defaultValue: 'dev', description: 'Environment where the code should be deployed')
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: '')
        booleanParam(name: 'RUN_MIGRATION', defaultValue: true, description: '')
    }
    
    stages {
        stage("Build") {
            steps {
                echo "Build the application"
                echo "Branch is ${env.BRANCH_NAME}"
            }
        }
        
        stage('Test') {
            when {
                expression {
                    params.EXECUTE_TESTS
                }
            }
            steps {
                dotnetTest project: 'CareerPath.sln', sdk: '.NET Linux SDK 6.0', logger: 'trx;logFileName=TestResult.trx', collect: 'XPlat Code Coverage'
                mstest testResultsFile:"**/TestResult.trx", keepLongStdio: true
            }
        }
        
        stage("Deploy") {
            steps {
                echo "Deploy the application"
//                 withCredentials([
//                 usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)]) {
//                     echo "Username: ${USER} and password ${PWD}"
//                 }
            }
        }
    }
}