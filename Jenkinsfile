node{

   def tomcatWeb = 'C:\\xampp\\tomcat\\webapps'
   def tomcatBin = 'C:\\xampp\\tomcat\\bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/AnmolAgnihotri/JenkinsWar.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      bat "${mvnHome}/bin/mvn package"
      }
      
  stage('SonarQube analysis') 
  {
    def scannerHome = tool 'sonar-qube';
    withSonarQubeEnv('sonar-qube1') 
    { 
    // If you have configured more than one global server connection, you can specify its name
      bat "${scannerHome}/bin/sonar-scanner"
    }
    }
    
   stage('Deploy to Tomcat'){
     bat "copy target\\JenkinsWar.war \"${tomcatWeb}\\JenkinsWar.war\""
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.bat"
         sleep(time:100,unit:"SECONDS")
   }
   
}
