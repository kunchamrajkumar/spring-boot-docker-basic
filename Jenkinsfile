node {
        def REPOSITORY = params.REPOSITORY
        def APPLICATION = params.APPLICATION
        def JFROG_REPO = params.JFROG_REPO
        stage ('checkout'){
           git branch: 'main', credentialsId: 'git_creds', url: 'https://github.com/kunchamrajkumar/spring-boot-docker-basic.git'
 
         }

       /*stage ('build'){ 
            withMaven(globalMavenSettingsConfig: '', jdk: 'java', maven: 'maven', mavenSettingsConfig: '', traceability: true) {
             sh 'mvn clean package'
           }
          }
        
       stage ('docker build image'){
              sh "docker build -t sample:latest ."
           }
   
       stage ('docker tag&Push image'){
             
               sh " docker login -u rajvam6806 -p Harshu@11  "
               sh "docker tag sample:latest rajvam6806/spring-boot-docker-basic:141 "
               sh " docker push rajvam6806/spring-boot-docker-basic:141 "
               sh " docker pull rajvam6806/spring-boot-docker-basic:141 "
           
          }*/
        
       /*stage ('tag & push to jfrog'){
            
           sh """
            
            docker login -u admin -p Password@123 https://kkumar.jfrog.io
            
             docker tag sample:latest $JFROG_REPO/$APPLICATION:$BUILD_NUMBER
             docker push $JFROG_REPO/$APPLICATION:$BUILD_NUMBER
             docker pull $JFROG_REPO/$APPLICATION:$BUILD_NUMBER
             """
          
       } */
       /*stage ('deploy'){
          def dockerRun = "docker run -d -p 8084:8000 $REPOSITORY/$APPLICATION:$BUILD_NUMBER"
         sshagent(['tomcat_ubuntu']) {
                 
            sh" ssh -o StrictHostKeyChecking=no ubuntu@3.88.26.89 ${dockerRun} "
            }
          } */

  /* stage ('deploy to k8s'){

            sshagent(['pem']) {
                    
            sh " scp -o stricthostkeychecking=no deployment.yaml ubuntu@3.82.119.174:/home/ubuntu"
                   
             sh " scp -o stricthostkeychecking=no service.yaml ubuntu@3.82.119.174:/home/ubuntu"       
             
              sh " ssh ubuntu@3.82.119.174  kubectl apply -f deployment.yaml"      
            sh " ssh ubuntu@3.82.119.174  kubectl apply -f service.yaml"          
           
   }

}*/
       stage (deploy){

             kubeconfig(credentialsId: 'KUBEconfig', serverUrl: 'http://3.82.119.174:8443') {
    
   sh "kubectl apply -f deployment.com"
}
       }



        
}
