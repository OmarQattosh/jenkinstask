pipeline{
	agent any
	parameters{
	string( name : 'R_IP' , defaultValue :'172.17.0.3' , description : ' slave ip address')
	}
	stages {
          stage('Deploy Dummy Script') {
            steps {
	      script {
	     sh " rm script.sh"	      
             sh " echo 'whoami' >> script.sh"
	     sh " echo 'free' >> script.sh"
             sh " echo 'id' >> script.sh"
	     sh " tar cf ${BUILD_NUMBER}.tar.gz script.sh"
             sh " scp ${BUILD_NUMBER}.tar.gz root@${params.R_IP}:/root" 
	       }	
              }
           }
        stage('Check Memory On Slave') {
		steps {
		    script{
			int mb = 1024*1024
Runtime runtime = Runtime.getRuntime()
	float perc = runtime.freeMemory() / runtime.totalMemory()
			    if ( perc < 0.8){
			    error (" build failed becuase of the thing")
 mail bcc: '', body: "<b>Build Failed</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'omarqattosh@gmail.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "omar.qattosh@exalt.ps"; 
			    }
			    

		    }
		    }
		}
           
		
		
         }
      }
