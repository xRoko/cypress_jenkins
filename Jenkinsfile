pipeline {

    agent any

    parameters {
        string(name: 'SPEC', defaultValue: "cypress/e2e/**/**", description: "Enter the script path that you want to execute")
        choice(name: 'BROWSER', choices:['chrome','edge', 'firefox'], description: "Choice the browser to execute your scripts")
    }

    stages{
        stage('Building') {
            steps{
                echo "Building the application"
            }

        }
        stage('Testing'){
            steps{
                bat "npm i"
                bat "npm install cypress --save-dev"
                bat "npx cypress run --browser ${BROWSER} --spec ${SPEC} --headless"
            }
        }
        stage('Deploying'){
            steps{
                echo "Deploying the application"
            }
        }
    }

    post {
        always{
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
        }
    }
}