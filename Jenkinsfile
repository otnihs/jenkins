node {

    stage('Clone sources') {
        git branch: 'Developement', url: 'https://github.com/otnihs/jenkins.git'
    }

    stage('Building images') {
        sh "sudo docker build . --no-cache -t otnihs/nginx:v2.2"
        sh "sudo docker push otnihs/nginx:v2.2"

    }

    stage('Deploying images') {
        sh "sudo kubectl apply -f ng-pod.yml"
        sh "sudo kubectl apply -f ng-service.yml"
    }

}
