node ("master") {
       stage 'Deploy'
       puppet.credentials 'secret'
	   echo "connection is made with puppet"
	   puppet.codeDeploy 'production' 
	   echo "connection not support"
} 