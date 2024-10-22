pipeline {
    agent any

    stages {

        stage('packaging') {
            steps {
                echo 'Building..'
                sh 'docker build -t $CI_REGISTRY_USER/demo1:test-2.0.0 -f ./Dockerfile .'
                sh 'docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD '
                sh 'docker tag $CI_REGISTRY_USER/demo1:test-2.0.0 $CI_REGISTRY_USER/demo1:test-3.0.0'
                sh 'docker push $CI_REGISTRY_USER/demo1:test-3.0.0'
            }
        }
    }
}