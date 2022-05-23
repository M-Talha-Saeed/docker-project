pipeline{

    agent any
    stages
    {
        stage('Clone Repo'){
            steps{
                script{
                    if(fileExists('/home/jenkins/.jenkins/workspace/docker-project/')){
                        dir('docker-project'){ sh 'git pull https://github.com/M-Talha-Saeed/docker-project.git main'}
                    }
                    else{
                        sh 'git clone https://github.com/M-Talha-Saeed/docker-project.git'
                    }
                }
            }
        }
        stage('Installs'){
            steps{
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Testing'){
            steps{
                sh 'cd api1 && python3 -m pytest --cov=application'
                sh 'cd api2 && python3 -m pytest --cov=application'
                sh 'cd api3 && python3 -m pytest --cov=application'
                sh 'cd api4 && python3 -m pytest --cov=application'
            }
        }
        stage('Build & Deploy'){
            steps{
                sh 'docker-compose build'
                sh 'docker-compose push'
            }
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose up -d'
            }
        }
    }
}