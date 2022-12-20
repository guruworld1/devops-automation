pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/guruworld1/devops-automation']]])
                sh 'mvn clean install'
                
        }
    }
    stage('Build docker image'){
        steps{
            script{
                sh 'docker build -t cmonkam/devops-integration .'
            }
        }
    }
    stage('Push image to Hub'){
        steps{
            script{
               withCredentials([string(credentialsId: 'dockerhub-id', variable: 'auto')]) {

                sh 'docker login -u cmonkam -p ${auto}'
}
                sh 'docker push cmonkam/devops-integration'
            }
        }
    }
    }
}











