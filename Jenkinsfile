
node()
{
    stage "Checkout Code"
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/siteshbade/nvnshoppingcart.git']]])
    
    stage "Build Code"
        sh "mvn clean package"
	
	stage "tomcat stop services"
		
		sh "sudo systemctl stop tomcat"
        
    stage "Deploy Application"
        //sh 'rm /var/lib/tomcat/webapps/nvnshoppingcart*'
        sh 'sudo cp **/*.war /opt/tomcat/webapps/'
	
	stage "tomcat stop services"
		sh "sudo systemctl start tomcat"
}
