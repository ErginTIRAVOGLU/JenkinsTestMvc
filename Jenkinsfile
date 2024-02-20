pipeline {
	agent any	
	stages {
		stage('Checkout Stage') {
			steps
			{
				git url: 'https://github.com/ErginTIRAVOGLU/JenkinsTestMvc.git', branch: 'main'
			}
		}		 
		stage('Release Stage') {
			steps 
			{
				bat 'net stop "w3svc"'
				bat "\"${tool 'MSBuild'}\" JenkinsTestMvc.sln /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:SkipInvalidConfigurations=true /t:build /p:Configuration=Release /p:Platform=\"Any CPU\" /p:DeleteExistingFiles=True /p:publishUrl=c:\\inetpub\\wwwroot\\JenkinsTestMvc"                        
				bat 'net start "w3svc"'
			}
		}
	}
}