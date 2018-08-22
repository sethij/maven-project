pipeline{
	agent any
	
	stages{
		stage('build'){
			steps{
				echo 'building..'
				bat 'mvn clean package'
			}
		}
	}
}