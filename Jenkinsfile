pipeline {
	agent any
	
	stages{
		
		stage("Build"){
			
			steps{
				
				bat 'mvn clean package'
			}
			
			post{
				
				success{
					echo 'Now Archiving'
					
					archiveArtifacts artifacts: '**/*.war'
				}
			}
			
		}
	
		stage("Deploy to Stage") {
		
			steps{
			
				build job: 'Deploy to Stage'
			}
			
		}
	
	}
	
}
	