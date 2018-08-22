pipeline{
	agent any
	
	tools{
		maven 'localMaven'
	}
	
	stages{
		stage('build'){
			steps{
				echo 'building..'
				bat 'mvn clean package'
			}
			post{
				success{
				echo 'Now archiving'
				archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		
		stage('deploy-to-staging'){
			steps{
				echo "deploying to staging"
				build job : 'deploy-to-staging'
			}
		}
		
		stage('deploy-to-production'){
			steps{
				timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
				echo "Deploying to production"
				build job: 'deploy-to-prod'
			}
			post{
				success{
					echo "Project Deployed to prod"
				}
				failure{
					echo "Project not deployed to prod"
				}
			}
		}
	
	}
}