
pipeline{

	agent any
	
	environment{
	 mvnHome= tool('MAVEN_HOME')
	 def tomcatWeb = 'C:\\opt\\apache-tomcat-8.5.64\\webapps'
	 def tomcatBin = 'C:\\opt\\apache-tomcat-8.5.64\\bin'
	 def tomcatStatus = ''
	}
	

	stages{
	
	   stage('SCM Checkout'){
		steps{
		 git 'https://github.com/siteshbade/nvnshoppingcart.git'
		 }
   }
   stage('Compile-Package-create-war-file'){
		steps{
      // Get maven home path
        
      bat "${mvnHome}/bin/mvn clean package sonar:sonar"
		}
      }
   stage ('Stop Tomcat Server') {
		steps{
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
				}
    }
   stage('Deploy to Tomcat'){
   
		steps{
     bat "copy target\\nvnshoppingcart.war \"${tomcatWeb}\\nvnshoppingcart.war\""
	 }
   }
      stage ('Start Tomcat Server') {
	  steps{
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.bat"
         sleep(time:100,unit:"SECONDS")
		 }
   }
	
	
	
	}
   
}