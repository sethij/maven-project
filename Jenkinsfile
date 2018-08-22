pipeline{
	agent any
	
	tools{
		maven 'localMaven'
	}
	stages{
		stage('build'){
			steps{
				echo 'building..'
				sh 'mvn clean package'
			}
		}
	}
}