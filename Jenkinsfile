pipeline{
	agent any
	parameters{
	string( name : 'R_IP' , defaultValue :'172.17.0.3' , description : ' slave ip address')
	}
	
	stages {
		stage('Clone sources') {
			steps {
				script{
        git branch: 'main', credentialsId: 'gitshit', url: 'https://github.com/OmarQattosh/jenkinstask.git'
				}
				}
		}
          stage('Deploy Dummy Script') {
            steps {
		    script {
	    
	     sh " tar cf ${BUILD_NUMBER}.tar.gz script.sh"
             sh " scp ${BUILD_NUMBER}.tar.gz root@${params.R_IP}:/root" 
	       }	
              }
           }
		   stage('unzip the file '){
			   steps{
				   
					    sh 'tar xf ${BUILD_NUMBER}.tar.gz'
					   sh 'chmod +x script.sh'
					   sh './script.sh'
				   
			   }
			   
		   }
        stage('Check Memory On Slave') {
		steps {
		    script{
			   
			Runtime runtime = Runtime.getRuntime()
			float perc = runtime.freeMemory() / runtime.totalMemory()
			    if ( perc > 0.8){
			     mail bcc: '', body: "<b>Build Failed</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'omarqattosh@gmail.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "omar.qattosh@exalt.ps"; 

				    error (" build failed becuase of the thing")
			    
			    }else {
	                  mail bcc: '', body: "<b>Build Succeed</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'omarqattosh@gmail.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "omar.qattosh@exalt.ps"; 
			  archiveArtifacts artifacts: '${BUILD_NUMBER}.tar.gz', followSymlinks: false
			    }
			    

		    }
		    }
		}
           
		
		
         }
      }
