pipeline{

agent any

stages{

stage('Checkout'){

steps{

git branch: "main", url: 'https://github.com/chiranjiv09/g2-spring-api-gateway.git'

}

}

stage('Build'){

steps{

sh 'chmod a+x mvnw'

sh './mvnw clean package -DskipTests=true'

}

post{

always{

archiveArtifacts 'target/*.jar'

}

}

}

stage('DockerBuild') {

steps {

sh 'docker build -t services/g2-api-gateway-service:latest .'

}

}

stage('Login') {

steps {

sh 'echo dockerhub123 | docker login -u kushck09 --password-stdin'

}

}

stage('Push') {

steps {

sh 'docker push kushck09/g2-api-gateway-service'

}

}

}

post {

always {

sh 'docker logout'

}

}

}
