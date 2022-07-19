pipeline{
	agent any
        stages {
          stage('Deploy Dummy Script') {
            steps {
	      script {
	     sh " rm script.sh"	      
             sh " echo 'whoami' >> script.sh"
	     sh " echo 'free' >> script.sh"
             sh " echo 'id' >> script.sh"
	     sh " tar cf ${BUILD_NUMBER}.tar.gz script.sh"
	         
	       
	       }
              	
              }
           }
         }
      }

