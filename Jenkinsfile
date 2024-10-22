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
    stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'gcloud version'
                sh 'gcloud compute zones list'
                sh 'gcloud config set container/use_client_certificate False'
                sh 'gcloud container clusters get-credentials $CI_GOOGLE_CLUSTER_NAME --zone $CI_GOOGLE_CLUSTER_ZONE --project $CI_GOOGLE_PROJECT_NAME'
                sh 'echo "$CI_REGISTRY_SECRET" > registry-dockerhub-secret.json '
                sh 'kubectl apply -f ./registry-dockerhub-secret.json'     
                sh 'kubectl apply -f ./deployment.yml'
                sh 'kubectl apply -f ./service.yml'
                echo 'Application successfully deployed. '
            }
        }
    } 
}       