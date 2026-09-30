pipeline {
 environment {
 imagename = "igross2026/jenkins-web1" // change the docker and image name
 image_tag    = "${BUILD_NUMBER}" // Sets version to current Jenkins build number
 registryCredential = 'igross2026' // docker credentails
 dockerImage = ''
 }
 agent any
 stages {
 stage('Cloning Git') {
 steps {
 git([url: 'https://github.com/IGross2022/jenkins-pipeline.git', branch: 'main']) // change the git url
 }
 }
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build imagename
 }
 }
 }
 stage('Running image') {
 steps{
 script {
 sh "docker run -itd -P ${imagename}:latest"
 }
 }
 }
 stage('Deploy Image') {
 steps{
 script {
 docker.withRegistry( '', registryCredential ) {
 dockerImage.push("$BUILD_NUMBER")
 dockerImage.push('latest')
 }
 }
 }
 }
 }
}
