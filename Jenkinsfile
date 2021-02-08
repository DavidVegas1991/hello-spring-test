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
					withGradle{
						configFileProvider([configFile(fileId: 'f7142cd7-9600-4ff9-a3fb-bc18db7c2a23', targetLocation: 'gradle.properties')]) {
    // some block
}
						
						{
							sh './gradlew sonarqube'			
						}
							
					}
			}
		}
	
	}
}