pipeline{
 tools{
        jdk 'Linux-java'
        maven 'M2_HOME'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/sibu610548/webapp.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		 sh 'mvn compile'
		}
		}
       stage("test"){
	    steps{
		 sh 'mvn test'
		}
		}
       stage("package"){
	    steps{
		 sh 'mvn clean package'
                 sh "mv target/*.war target/myweb.war"

		}
		}
   stage("deploy"){
	   steps{

      sshagent(['devops']) {

	        sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@13.232.158.230:/home/ec2-user/tomcat-10/webapps/

              ssh ec2-user@13.232.158.230 /home/ec2-user/tomcat-10/bin/shutdown.sh
               ssh ec2-user@13.232.158.230 /home/ec2-user/tomcat-10/bin/startup.sh
            
          
          """

}

	   
		}
		  
	  }

// stage(backup)
// 		 {
//   steps{

// 	  nexusArtifactUploader artifacts: [[artifactId: 'idream-it-solutions', classifier: '', file: 'target/myweb.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.idream.webapp', nexusUrl: '3.110.167.8:8080/nexus/', nexusVersion: 'nexus2', protocol: 'http', repository: 'repoR', version: '1.1'
	  
//   }
	
// }
	}
	}
