pipeline {
    //Where the agent will run the pipeline (master or slave)
    //agent any
    //or we can specfy the agent as below
    agent {lable 'worker'}
    stages {
        stage('First Build') {
            steps{
                sh "echo Hello world"
                sh "echo more steps"
            }
        }
        stage9'second stage'){
            steps{
                sh "echo second stage"
            }
        }
    }   
}