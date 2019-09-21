node {

    stage('Clone sources') {
        git url: 'https://github.com/otnihs/jenkins.git'
    }

    stage('Building images') {
        sh "sudo docker build . -t otnihs/nginx:v1"
        sh "sudo docker push otnihs/nginx:v1"

    }

    stage('Deploying images') {
        sh "sudo kubectl apply -f ng-pod.yml"
        sh "sudo kubectl apply -f ng-service.yml"
    }

}
