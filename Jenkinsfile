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
		}
	}
}