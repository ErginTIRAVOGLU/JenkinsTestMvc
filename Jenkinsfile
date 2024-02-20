pipeline 
{
	agent any
	environment 
	{
        dotnet = 'C:\\Program Files\\dotnet\\dotnet.exe'
    }
	stages 
	{
		stage('Checkout Stage')
		{
			steps
			{
				git url: 'https://github.com/ErginTIRAVOGLU/JenkinsTestMvc.git', branch: 'main'
			}
		}
		stage('Build Stage') 
		{
            steps {
                bat 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\AspDotNetJenkins-Pipeline\\JenkinsTestMvc.sln --configuration Release'
            }
        }
		stage('Release Stage') 
		{
			steps 
			{
				bat 'net stop "w3svc"'
				bat "\"${tool 'MSBuild'}\" JenkinsTestMvc.sln /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:SkipInvalidConfigurations=true /t:build /p:Configuration=Release /p:Platform=\"Any CPU\" /p:DeleteExistingFiles=True /p:publishUrl=c:\\inetpub\\wwwroot\\JenkinsTestMvc"                        
				 bat 'net stop "w3svc"'
			}
		}
	}
}