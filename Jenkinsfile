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
			    import jenkins.model.*
jenkins = Jenkins.instance
	      int mb = 1024*1024
Runtime runtime = Runtime.getRuntime()
out.println (runtime.freeMemory() / mb);
out.println runtime.totalMemory() / mb
out.println runtime.maxMemory() / mb
		    }
		    }
		}
           
		
		
         }
      }
