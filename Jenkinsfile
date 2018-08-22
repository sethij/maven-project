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
	
	}
}