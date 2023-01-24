node{
def mavenHomedir= tool name: "Maven"
//echo "Build Number: ${env.BUILD_NUMBER}"
echo "Job Name: ${env.JOB_NAME}"
echo "node:${env.NODE_NAME}"
stage('sourceCodefromGit'){
git branch: 'development', credentialsId: '0af9a5cd-3c8a-4b87-aaa3-5e08f8b3b874', url: 'https://github.com/NaveenSai1605/maven-web-application.git'
}
stage('mavenBuilt'){
sh "${mavenHomedir}/bin/mvn clean package"
}
stage('artifactToNexus'){
sh "${mavenHomedir}/bin/mvn clean deploy"
}
stage('sonarQubeReport'){
sh "${mavenHomedir}/bin/mvn sonar:sonar"
}
stage('deployToTomcat'){
sshagent(['fc4fa3fc-bb2b-483d-b097-9fc9ea2a7616']) {
    // some block
}
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@43.205.217.240:/opt/apache-tomcat-9.0.70/webapps/"
}

}
