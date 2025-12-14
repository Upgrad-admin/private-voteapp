pipeline {
    agent { label 'built-in' }

    options {
        buildDiscarder(logRotator(numToKeepStr: '15'))      // keep last 15 builds [web:8]
        disableConcurrentBuilds()                           // prevent parallel runs [web:9]
        retry(2)                                            // retry failed stages twice [web:9]
        timeout(time: 20, unit: 'MINUTES')                  // global timeout [web:9]
    }

    parameters {
        string(
            name: 'BRANCH',
            defaultValue: 'main',
            description: 'branch to build'
        )                                                  // string parameter example [web:9]
        choice(
            name: 'ENV',
            choices: ['qa', 'dev', 'prod'],
            description: 'env to build'
        )                                                  // static choice parameter [web:7]
    }

    stages {

        stage('Docker login and push') {
            steps {
                sh 'docker login -u nisarga2403 -p Nisarga24*'                 // docker login [web:6]
                sh 'docker build -t nisarga2403/votes:${BUILD_NUMBER} .'        // docker build example [web:6]
                sh 'docker push nisarga2403/votes:${BUILD_NUMBER}'              // docker push with build tag [web:6]
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo starting deployment'                                 // placeholder deploy step [web:6]
            }
        }
    }
}
