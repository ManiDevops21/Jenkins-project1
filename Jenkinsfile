Jenkinsfile (Declarative Pipeline)
pipeline {
    agent {
        Puppet { 'sudo yum -y install http://yum.puppetlabs.com/puppetlabs-release-el-7.noarch.rpm'
	         'sudo yum -y install puppet' }
    }
    stages { 
        stage('Test') {
            steps {
		
                sh 'systemctl status puppet'
            }
	}
       	 stage('Config') {
            steps {
		
                'puppet agent --test --ca_server=puppet.example.com'
		'puppetserver ca list'
		'puppetserver ca sign --certname server1'
            }
	}
       	 stage('Test config') {
            steps {
		
                'sudo vi /etc/puppetlabs/code/environments/production/manifests/createuser.pp'
		'user { 'puppetuser':
   		 ensure     => present,
   		uid        => '1020',
		 shell      => '/bin/bash',
 		 home       => '/home/puppetuser',
 		managehome => true,
		}'
		'sudo systemctl restart puppet'
		'less /etc/passwd | grep -i puppetuser'
		'puppet apply /etc/puppetlabs/code/environments/production/manifests/createuser.pp'
            }	
  	  }
	}
      } 
