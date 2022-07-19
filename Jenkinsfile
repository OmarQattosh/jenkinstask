pipeline{
	agent any
        stages {
          stage('Deploy Dummy Script') {
            steps {
             sh 'echo 'whoami' >> script.sh'
	     sh 'echo 'free' >> script.sh'
             sh ' tar cf BUILD_NUMBER.tar.gz'
	       
              	
              }
           }
         }
      }

