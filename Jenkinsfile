node{
      def dockerImageName= 'arashy76/javadedockerapp_$JOB_NAME:$BUILD_NUMBER'
      stage('SCM Checkout'){
         git 'https://github.com/arashy76/java-groovy-docker'
      }
      stage('Build'){
         // Get maven home path and build
         //def mvnHome =  tool name: 'Apache Maven 3.6.3', type: 'maven'   
         //sh "${mvnHome}/bin/mvn package -Dmaven.test.skip=true" 
         sh "/usr/share/maven/bin/mvn package -Dmaven.test.skip=true" 
      }       
     
     stage ('Test'){
         //def mvnHome =  tool name: 'Maven 3.6.3', type: 'maven'    
         //sh "${mvnHome}/bin/mvn verify; sleep 3"
         sh "/usr/share/maven/bin/mvn verify; sleep 3"
      }
      
     stage('Build Docker Image'){         
           sh "docker build -t ${dockerImageName} ."
      }  
   
      stage('Publish Docker Image'){
         withCredentials([string(credentialsId: 'dockerpwdarashy76', variable: 'dockerPWD')]) {
              sh "docker login -u arashy76 -p ${dockerPWD}"
         }
        sh "docker push ${dockerImageName}"
      }
      
    //stage('Run Docker Image'){
    //        def dockerContainerName = 'javadockerapp_$JOB_NAME_$BUILD_NUMBER'
    //        sh "sudo docker run -p 8082:8080 -d --name ${dockerContainerName} ${dockerImageName}"
      
    //}
      stage('Run Docker Image'){
            def dockerContainerName = 'javadockerapp_$JOB_NAME_$BUILD_NUMBER'
            def changingPermission='sudo chmod +x stopscript.sh'
            def scriptRunner='sudo ./stopscript.sh'           
            def dockerRun= "sudo docker run -p 8082:8080 -d --name ${dockerContainerName} ${dockerImageName}" 
            withCredentials([string(credentialsId: 'deploymentserverpwd', variable: 'dpPWD')]) {
                  sh "sshpass -p ${dpPWD} ssh -o StrictHostKeyChecking=no arash@127.0.0.1"
                  sh "sshpass -p ${dpPWD} scp -r stopscript.sh arash@127.0.0.1:/home/arash" 
                  sh "sshpass -p ${dpPWD} ssh -o StrictHostKeyChecking=no arash@127.0.0.1 ${changingPermission}"
                  sh "sshpass -p ${dpPWD} ssh -o StrictHostKeyChecking=no arash@127.0.0.1 ${scriptRunner}"
                  sh "sshpass -p ${dpPWD} ssh -o StrictHostKeyChecking=no arash@127.0.0.1 ${dockerRun}"
            }
            
      
      }
         
  }
      
