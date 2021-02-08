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
						configFileProvider([configFile(fileId: 'gradle.properties', variable: 'gradle.properties')])
						{
							sh './gradlew clean sonarqube'			
						}
							
					}
			}
		}
	
	}
}