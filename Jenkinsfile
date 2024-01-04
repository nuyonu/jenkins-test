pipeline {
    agent any
    
    stages {
        stage("build") {
            steps {
                echo "Build the application"
                echo "${BRANCH_NAME}"
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
                echo "${BRANCH_NAME}"
            }
        }
        
        stage("deploy") {
            steps {
                echo "Deploy the application"
                echo "${BRANCH_NAME}"
            }
        }
    }
}