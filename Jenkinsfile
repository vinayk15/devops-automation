pipeline {
    agent any
    tools{
        maven '3.8.2'
    }
    stages{
        stage('Build Maven'){
            steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vinayk15/devops-automation']]])
                sh 'mvn clean install'
            }
        }
		stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t javadev/devops-build .'
                }
            }
        }
        	stage('Push Image to Hub'){
            steps{
                script{

                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u vinaydocker15 -p ${dockerhubpwd}'
					sh 'docker push javadev/devops-build'
                }

                }
            }
        }
	}
}