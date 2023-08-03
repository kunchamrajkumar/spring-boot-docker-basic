node {

  stage ('checkout'){
           git branch: 'main', credentialsId: 'git_creds', url: 'https://github.com/kunchamrajkumar/spring-boot-docker-basic.git'
 
         }

   stage ('build'){ 
        withMaven(globalMavenSettingsConfig: '', jdk: 'java', maven: 'maven', mavenSettingsConfig: '', traceability: true) {
    sh 'mvn clean package'
           }
   }
     stage ('docker build'){

       sh "docker build -t sample:latest ."
     }
   
   stage ('docker tag&Push'){
      withCredentials([usernamePassword(credentialsId: 'docker_creds', passwordVariable: 'DockerPasswd', usernameVariable: 'Dockeruser')]) {
    
    
     sh " docker login "
         sh "docker tag sample:latest rajvam6806/spring-boot-docker-basic:v1 "
     sh " docker push rajvam6806/spring-boot-docker-basic:v1 "
   }
   }

stage ('deploy'){
   def dockerRun=docker run -d -p 8084:8000 rajvam6806/spring-boot-docker-basic:v1
  sshagent(['tomcat_ubuntu']) {
   
     sh" ssh -o StrictHostKeyChecking=no ubuntu@52.90.52.155 ${dockerRun} "
}
}



}
