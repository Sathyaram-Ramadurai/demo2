node{
      def dockerImageName= 'arashy76/javadedockerapp_$JOB_NAME:$BUILD_NUMBER'
      stage('SCM Checkout'){
         git 'https://github.com/Sathyaram-Ramadurai/demo2'
      }
      stage('Build'){
         // Get maven home path and build
         //def mvnHome =  tool name: 'Apache Maven 3.6.3', type: 'maven'   
         //sh "${mvnHome}/bin/mvn package -Dmaven.test.skip=true" 
         sh "C:/Users/10433/Downloads/apache-maven-3.9.2-bin/apache-maven-3.9.2/bin/mvn package -Dmaven.test.skip=true" 
      }       
     
     stage ('Test'){
         //def mvnHome =  tool name: 'Maven 3.6.3', type: 'maven'    
         //sh "${mvnHome}/bin/mvn verify; sleep 3"
         sh "C:/Users/10433/Downloads/apache-maven-3.9.2-bin/apache-maven-3.9.2/bin/mvn verify; sleep 3"
      }
      
     stage('Build Docker Image'){         
           sh "docker build -t demo2 ."
      }  
   
      
    //stage('Run Docker Image'){
    //        def dockerContainerName = 'javadockerapp_$JOB_NAME_$BUILD_NUMBER'
    //        sh "sudo docker run -p 8082:8080 -d --name ${dockerContainerName} ${dockerImageName}"
      
    //}
      
    stage('Run Docker Image'){
            sh "docker run demo2"
      }
         
  }
      
