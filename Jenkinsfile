node {

    stage('Clone sources') {
        git branch: 'Developement', url: 'https://github.com/otnihs/jenkins.git'
    }

    stage('Building images') {
        sh "sudo docker build . --no-cache -t otnihs/nginx:v2.4"
        sh "sudo docker push otnihs/nginx:v2.4"

    }

    stage('Deploying images') {
        sh "sudo kubectl apply -f ng-pod.yml"
        sh "sudo kubectl apply -f ng-service.yml"
    }

}

script {
       def scannerHome = tool 'sonarqube';
          withSonarQubeEnv("sonarqube-server") {
           sh "${tool("sonarqube")}/bin/sonar-scanner \
           -Dsonar.projectKey=${sonarid} \
           -Dsonar.projectName=${appname} \
           -Dsonar.projectVersion=${currver} \
           -Dsonar.issuesReport.html.enable=true \
           -Dsonar.issuesReport.html.location=./ \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=${env.SONAR_HOST_URL} \
           -Dsonar.login=${env.SONAR_AUTH_TOKEN}"
               }
           }
