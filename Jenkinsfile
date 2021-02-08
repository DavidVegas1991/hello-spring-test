
pipeline {
    agent any
    stages {

        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew clean test' 
                }


            }
            post{
                always{
                    junit 'build/test-results/**/TEST-*.xml'
	            recordIssues(
			enabledForFailure: true, aggregatingResults: true,
			tools: [java(), checkStyle(pattern: 'build/reports/checkstyle/*.xml', reportEncoding: 'UTF-8')]
		    )

                    
                    publishHTML (target: [
                        alwaysLinkToLastBuild: true,
                        
                        keepAll: true,
                        reportDir: 'build/reports/',
                        reportFiles: '*.html',
                        reportName: 'My Reports David',
                        reportTitles: 'The Report'
                    ])
		    publishHTML (target: [
                        
                        
                        
                        reportDir: 'build/reports/checkstyle',
                        reportFiles: 'test.html',
                        reportName: 'My Reports checkstyle David',
                        reportTitles: 'The Report'
                    ])
                }
            }
           
        }
        
        
    }
    
}

