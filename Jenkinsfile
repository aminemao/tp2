pipeline {

   agent any

   tools{
      maven 'Maven install'
   }

   stages {
      stage('Clone') {
         steps {
            checkout([$class: 'GitSCM',
                branches: [[name: '*/master' ]],
                extensions: scm.extensions,
                userRemoteConfigs: [[
                    url: 'https://github.com/aminemao/tp2.git',
                    credentialsId: '471dbd6c-2b77-4884-a655-15a6ea2a278c'
                ]]
            ])

            //List all directories
            sh "ls -lart ./*"
         }
      }
	  stage('Compile'){
         steps{
            withMaven(maven:'Maven install')
            {
              sh "mvn compile"
            }
         }
      }
      stage('Test'){
         steps{
            withMaven(maven:'Maven install')
            {
              sh "mvn test"
            }
         }
         
      }
      
      stage('Build'){
         steps{
            sh "mvn -B -DskipTests clean install"
         }
      }
	  
	       
      
	stage('Code Coverage') {
        steps {
            sh 'mvn clean cobertura:cobertura'
        }
        
        post {
	        always {
	            step([$class: 'CoberturaPublisher', autoUpdateHealth: true, autoUpdateStability: true, coberturaReportFile: '**/target/site/cobertura/*.xml', failUnhealthy: false, failUnstable: false, maxNumberOfBuilds: 2, onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: true])
	        }
	    }
    }
	
	stage ('SonarQube analysis') {
         steps {
            withSonarQubeEnv(installationName: 'sonarQube Connect', credentialsId: 'a4e496bb-bdb8-4151-abdd-934973642375') {
               sh 'mvn clean sonar:sonar -Dsonar.login=$Login -Dsonar.password=$Password'
            }
         }
      }


	}
}