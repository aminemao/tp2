pipeline {
	agent any
	stages {
	    stage("STAGE 1") {
		 steps {
			echo "first step"
			echo "second step"
		 }		 
		}
		stage("STAGE 2") {
		 steps {
			echo "first step"
			echo "second step"
		 }
		}
		
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

	}
}