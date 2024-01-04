pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'Execute tests', defaultValue: true, description: '')
        booleanParam(name: 'Run Sonar Scan', defaultValue: true, description: '')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'stg', 'prod'], defaultValue: 'dev', description: 'Environment where the code should be deployed')
        string(name: 'Branch', defaultValue: 'main', description: '')
        booleanParam(name: 'Run migration', defaultValue: true, description: '')
    }
    
    stages {
        stage("Build") {
            steps {
                echo "Build the application"
                echo "Branch is ${env.BRANCH_NAME}"
            }
        }
        
        stage("Test") {
            when {
                expression {
                    env.BRANCH_NAME == 'dev'
                }
            }
            steps {
                echo "Test the application"
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