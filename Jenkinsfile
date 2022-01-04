
pipeline {
agent any
		stages {
		
		stage ('Jenkins-Master') {
			    agent {
		               label {
		                       label "built-in"   
		                     }     
		                } 
					steps {
							dir ("/mnt/"){
                                                                sh "rm -rf SCM SCM@tmp"  
							           sh "git clone https://github.com/saurabhpathe/SCM.git -b master"
							           sh "cp -r new-pair.pem /mnt/SCM"
							}
							dir ("/mnt/SCM"){
							           sh "scp -r -i new-pair.pem indexa.html ec2-user@10.0.2.181:/var/www/html/"
						
							            sh "scp -r -i new-pair.pem indexb.html ec2-user@10.0.3.111:/var/www/html/"
							
							}
					      }
 			    } 

		
			stage ('Slave-1') {
			     agent {
		              label {
		                      label "Slave-1"
				                customWorkspace "/home/ec2-user/"  
		                    }
		                } 
					steps {
						
						  sh "sudo chmod -R 777 /var/www/html"
						
						        sh "sudo mv /var/www/html/indexa.html /var/www/html/index.html"  
						
						
						  sh "sudo service httpd start"
					    } 
				
					
			       }
				  }
			
			stage ('Slave-2') {
			     agent {
		              label {
				               label "Slave-2"
					             customWorkspace "/home/ec2-user/"   
			                 }
			              }
			      steps {
				       
						  sh "sudo chmod -R 777 /var/www/html"
						
						   sh "sudo mv /var/www/html/indexb.html /var/www/html/index.html"   
					   
				
						    sh "sudo service httpd start"
					    }
				
					 
				    }
			}	  
	
 
