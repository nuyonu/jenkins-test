pipeline {
    agent any
    
    stages {
        stage("build") {
            steps {
                echo "Build the application"
                echo "Branch is ${env.BRANCH_NAME}"
            }
        }
        
        stage("test") {
            when {
                expression {
                    env.BRANCH_NAME == 'dev'
                }
            }
            steps {
                echo "Test the application"
            }
        }
        
        stage("deploy") {
            steps {
                echo "Deploy the application"
            }
        }
    }
}