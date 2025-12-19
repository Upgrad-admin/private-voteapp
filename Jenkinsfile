pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '15')) 
        disableConcurrentBuilds()
        retry(2)
        timeout(time: 20, unit: 'MINUTES')
    }
    parameters{
        string(name: 'BRANCH', defaultValue: 'main', description: 'branch to build') 
        choice(name: 'ENV', choices: ['qa', 'dev', 'prod'], description: 'env to build') 
    }
    stages{
        stage("Docker login and push"){
            steps{
                sh "docker login -u nisarga2403 -p Nisarga24*"
                sh '''
                    cd vote
                    docker build -t nisarga2403/vote:v${BUILD_NUMBER} .
                    '''
                sh "docker push nisarga2403/vote:v${BUILD_NUMBER}"
            }
        }
        stage("Test"){
            agent{label 'linux'}
            steps{
                sh "echo linux test"
                sh "sleep 100"
            }
        }
        stage("Test2"){
            agent{label 'windows'}
            steps{
                sh "echo window test"
                sh "sleep 100"
            }
        }
        stage("deploy"){
            steps{
                sh "echo starting deployment"
            }
        }

    }
}
    
