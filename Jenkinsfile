pipeline {
	
	agent any
    
    tools 
    {
        maven "MAVEN_HOME"
    }
    
    environment 
    {
         mvnHome = "C:\\Maven"
    }
	 
	 stages
	 { 
		// stage('Preparation')
		// {
		  // steps 
           // {
            //  def mvnHome
		      // mvnHome = tool 'M3'
            // }
		// }
		
		stage('Build and Scan')
		{
			steps 
			{
				bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean compile package/)
			}
			post
			{
				failure
				{
					echo 'build fail'
				}
				
				success
				{
					echo 'Now Archiving the war file...'
                    archiveArtifacts artifacts: '**/target/*.war'
				}
				
				
			}
			
		}
		
		stage ('Deploy')
		{
			 steps 
			 {
				build job: 'deploy-insecure-bank-app'
			 }
		}
	 
	 }
	 
}
