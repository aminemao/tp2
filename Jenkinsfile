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
	}
}