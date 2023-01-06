pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url:'https://github.com/longmaikel/Vue.js-unit-test-with-jest.git', branch: 'master'
            }
        }
        stage('Dependencies') {
            steps {
                sh 'docker build -f ./.docker/Dockerfile.dep -t project_dep .'
                sh 'sudo docker run --rm -v ${PWD}:/app project_dep'
            }
        }
        stage('Test') {
            steps {
                sh 'sudo docker build -f ./.docker/Dockerfile.test -t project_test .'
                sh 'sudo docker run --rm -v ${PWD}:/app project_test'
            }
        }
        stage('Build') {
            steps {
                sh 'sudo docker build -f ./.docker/Dockerfile.build -t project_build .'
                sh 'sudo docker run --rm -v ${PWD}:/app project_build'
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo docker build -f ./.docker/Dockerfile.run -t project_run .'
                sh 'sudo docker run -it -d -p 1137:80  project_run'
            }
        }

    }
}
