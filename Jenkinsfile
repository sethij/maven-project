pipeline{
	agent any
	
	tools{
		maven 'localMaven'
	}
	
	parameters{
		string(name: 'tomcat_dev', defaultValue: 'D:\\apache-tomcat-8.5.32\\webapps\\', description: 'Staging server' )
		string(name: 'tomcat_prod', defaultValue: 'D:\\apache-tomcat-8.5.32_prod\\webapps\\', description: 'Staging server' )
	}
	
	triggers{
		pollSCM('* * * * *');
	}
	
	stages{
		stage('Build'){
			steps{
				echo 'Building..'
				bat 'mvn clean package'
			}
			post{
				success{
					echo 'Archieving...'
					archieveArtifact artifacts: '**/target/*.war'
				}
			}
		}
		stage('Deploy'){
			parallel{
				stage('Deploy to staging'){
					steps{
						echo 'Deploying to staging'
						bat 'xcopy **/target/*.war ${params.tomcat_dev}'
					}
				}
				stage('Deploy to staging'){
					steps{
						echo 'Deploying to prod'
						bat 'xcopy **/target/*.war ${params.tomcat_prod}'
					}
				}
				
			}
		}
	}
}