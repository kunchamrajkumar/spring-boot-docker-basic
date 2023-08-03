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

     sh "docker tag sample:latest spring-boot-docker-basic:v1 "
     sh " docker login -u rajvam6806 -p Harshu@11"
   }
  





}
