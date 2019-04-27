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
			
				build job: 'Deploy-to-Stage'
			}
			
		}
		
		stage("Deploy to Production"){
		
			steps{
					
				timeout (time: 5, unit: DAYS){
					input message: 'Approve Production Deployment'
				}
				
				build job:'Deploy-to-Production'
			}
			
			post{
				
				success{
					
					echo 'Deployment on PRODUCTION is Successful'
				}
				
				failure{
					
					echo 'Deployment failure on PRODUCTION'
				}
			}
		}
	}
}
	