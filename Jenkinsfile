pipeline{
	agent any
	stages{
		stage('Test'){
			steps{
				withGradle{
					sh './gradlew clean test check'
				}
			}
			post{
				always{
					junit 'build/test-results/test/TEST-*.xml'
					recordIssues enabledForFailure: true,
					tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
				}
			}
	
		}
		stage('QA'){
			steps{
				withGradle{
					sh './gradlew check'
				}
			}
			
			post{
				always{
					
					recordIssues enabledForFailure: true,
					tool: pmdParser(pattern: 'build/reports/pmd/*.xml')

				}
			}
		}	
		stage('sonarqube'){
			steps{
					stage('sonarqube credentials'){
			                withSonarQubeEnv(credentialsId: 'e8ebb9a1-7ea1-42ba-aaa5-76978e6bb86b', installationName: 'local') 
                            {
					            sh './gradlew sonarqube'		
				            }
		            }
			}
		}

	
	}
}