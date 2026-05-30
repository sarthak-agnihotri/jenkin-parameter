pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    parameters{
        choice(
            name: 'ACTION',
            choices: ['compile','test','package','all'],
            description: 'Choose build action'
        )
        string(
            name: 'MESSAGE',
            defaultValue: 'Hello Jenkins',
            description: 'Custom message'
        )
    }
    environment{
        PROJECT_NAME="jenkin-parameter"
    }
    stages{
        stage('Checkout'){
            steps{
                git branch: 'main',
                url: 'https://github.com/sarthak-agnihotri/jenkin-parameter.git'
            }
        }
        stage('Info'){
            steps{
                bat 'echo Project = %PROJECT_NAME%'
                bat 'echo Message = %MESSAGE%'
            }
        }
        stage('Compile'){
            when{
                expression{params.ACTION=='compile'||params.ACTION=='all'}
            }
            steps{
                bat 'mvn clean compile'
            }
        }
        stage('Test'){
            when{
                expression{params.ACTION=='test'||params.ACTION=='all'}
            }
            steps{
                bat 'mvn test'
            }
        }
        stage('Package'){
            when{
                expression{params.ACTION=='package'||params.ACTION=='all'}
            }
            steps{
                bat 'mvn package'
            }
        }
    }
    post{
        success{
            echo "BUILD SUCCESS"
        }
        failure{
            echo "BUILD FAILED"
        }
        always{
            echo "Pipeline finished"
        }
    }
}