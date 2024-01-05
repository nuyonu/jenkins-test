pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'EXECUTE_TESTS', defaultValue: true, description: '')
        booleanParam(name: 'RUN_SONAR_SCAN', defaultValue: true, description: '')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'stg', 'prod'], description: 'Environment where the code should be deployed')
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: '')
        booleanParam(name: 'RUN_MIGRATION', defaultValue: true, description: '')
    }
    
    environment {
        GITHUB_URL = 'https://github.com/nuyonu/jenkins-test'
        GITHUB_CREDENTIALS_NAME = 'nuyonu-github-username-PAT'
    }
    
    stages {
        stage("Checkout") {
           steps {
                git branch: "${BRANCH_NAME}", credentialsId: env.GITHUB_CREDENTIALS_NAME, url: env.GITHUB_URL
           }
        }
        
        stage("Build") {
            steps {
                dotnetBuild project: 'WebApplication3.sln', sdk: '.NET 8 Linux'
            }
        }
        
        stage('Test') {
            when {
                expression {
                    params.EXECUTE_TESTS
                }
            }
            steps {
                dotnetTest noBuild: true, logger: 'trx;LogFileName=UnitTests.trx', project: 'WebApplication3.sln', sdk: '.NET 8 Linux'
                xunit checksName: '', tools: [MSTest(excludesPattern: '', pattern: '**/*.trx', skipNoTestFiles: true, stopProcessingIfError: true)]
            }
        }
        
        stage("Deploy") {
            steps {
                echo "Deploy the application"
            }
        }
    }
}