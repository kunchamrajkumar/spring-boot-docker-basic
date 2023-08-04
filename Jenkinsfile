node {
        def REPOSITORY = params.REPOSITORY
        def APPLICATION = params.APPLICATION
        def JFROG_REPO = params.JFROG_REPO
        stage ('checkout'){
           git branch: 'main', credentialsId: 'git_creds', url: 'https://github.com/kunchamrajkumar/spring-boot-docker-basic.git'
 
         }

       stage ('build'){ 
            withMaven(globalMavenSettingsConfig: '', jdk: 'java', maven: 'maven', mavenSettingsConfig: '', traceability: true) {
             sh 'mvn clean package'
           }
          }
        
       stage ('docker build image'){
              sh "docker build -t sample:latest ."
           }
   
       stage ('docker tag&Push image'){
             
               sh " docker login -u rajvam6806 -p Harshu@11  "
               sh "docker tag sample:latest $REPOSITORY/$APPLICATION:$BUILD_NUMBER "
               sh " docker push $REPOSITORY/$APPLICATION:$BUILD_NUMBER "
               sh "docker logout"
           
          }
        
       stage ('tag & push to jfrog'){
            
           sh """
            
            docker login -u admin -p Password@123 https://kkumar.jfrog.io
            
             docker tag sample:latest $JFROG_REPO/$APPLICATION:$BUILD_NUMBER
             docker push $JFROG_REPO/$APPLICATION:$BUILD_NUMBER
             docker pull $JFROG_REPO/$APPLICATION:$BUILD_NUMBER
             """
          
       }
       stage ('deploy'){
          def dockerRun = "docker run -d -p 8084:8000 $REPOSITORY/$APPLICATION:$BUILD_NUMBER"
         sshagent(['tomcat_ubuntu']) {
                 sh"docker stop $(docker ps -q) )"
                 sh "docker rm $(docker ps -q) "
            sh" ssh -o StrictHostKeyChecking=no ubuntu@3.88.26.89 ${dockerRun} "
            }
          }



}
