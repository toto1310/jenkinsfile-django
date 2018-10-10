pipeline {
    agent {
        docker {
            image 'python:3-alpine'
        }
    }
    // environment {
        // workDir = 'example/maven'
    // }

    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('Test') {
            steps {
                sh 'pip install pipenv'
                sh 'pipenv install --dev'
                sh 'pipenv run tests'
                junit 'nosetests.xml'
                cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
            }
        }
        stage('Lint') {
            steps {
                sh 'pipenv run lint'
                warnings canResolveRelativePaths: false, canRunOnFailed: true, categoriesPattern: '', consoleParsers: [[parserName: 'PyLint']], defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', messagesPattern: '', unHealthy: ''
            }
        }
    }
}