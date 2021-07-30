pipeline {
    options {
        disableConcurrentBuilds()
    }
    
    agent any

    environment {
        BUILD_URL = "${BUILD_URL}"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy project...'
            }
        }
        }
        post {
            always {
                influxDbPublisher(selectedTarget: 'TestDB', customData: assignURL(BUILD_URL))
                echo 'The extra random stuff...'
                influxDbPublisher(selectedTarget: 'TestDB', customData: reportMetric())
            }
        }
    }

def assignURL(build_url) {
    def buildURL = [:]
    buildURL['url'] = build_url
    return buildURL
}

def reportMetric() {
    def myFields = [:]
    Random rnd = new Random()
    myFields['random_build_metric'] = rnd.nextInt(100)
    return myFields
}
