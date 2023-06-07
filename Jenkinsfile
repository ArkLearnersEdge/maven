pipeline
{
		agent any
		stages
		{
			stage('download')
			{
				steps
				{
					script
					{
						try
						{
							git 'https://github.com/ArkLearnersEdge/maven.git'
						}
						catch(Exception e1)
						{
							mail bcc: '', body: 'error E1 related to ', cc: 'developer@gail.com, rm@gmail.com', from: '', replyTo: '', subject: 'Download', to: 'scrum@gmail.com'
						}
					}
				}
				
			}
			stage('BUild')
			{
				steps
				{
					script
					{
						try
						{
							sh 'mvn package'
						}
						catch(Exception e2)
						{
							mail bcc: '', body: 'error E2 related to ', cc: 'developer@gail.com, rm@gmail.com', from: '', replyTo: '', subject: 'Download', to: 'scrum@gmail.com'
						}
					}
				}
				
			}
			stage('Deploy')
			{
				steps
				{
					script
					{
						try
						{
							deploy adapters: [tomcat9(credentialsId: '938519d4-ff73-4d7b-8a43-1d928cc910ca', path: '', url: 'http://172.31.41.140:8080')], contextPath: 'testapp', war: '**/*.war'	
						}
						catch(Exception e3)
						{
							mail bcc: '', body: 'error E3 related to ', cc: 'developer@gail.com, rm@gmail.com', from: '', replyTo: '', subject: 'Download', to: 'scrum@gmail.com'
						}
					}
				}
				
			}
			stage('Testing')
			{
				steps
				{
					script
					{
						try
						{
							git 'https://github.com/ArkLearnersEdge/FunctionalTesting.git'
							sh 'java -jar /home/ubuntu/.jenkins/workspace/sp_test/testing.jar'
							
							
						}
						catch(Exception e4)
						{
							mail bcc: '', body: 'error E4 related to ', cc: 'developer@gail.com, rm@gmail.com', from: '', replyTo: '', subject: 'Download', to: 'scrum@gmail.com'
						}
					}
				}
				
			}
		}
		post
		{
			success
			{
			
				deploy adapters: [tomcat9(credentialsId: '938519d4-ff73-4d7b-8a43-1d928cc910ca', path: '', url: 'http://172.31.42.164:8080')], contextPath: 'testapp', war: '**/*.war'	
			}
			failure
			{
				mail bcc: '', body: 'production failed ', cc: 'developer@gail.com, rm@gmail.com', from: '', replyTo: '', subject: 'Download', to: 'scrum@gmail.com'
			}
			
		}
	
}
