

node ("master") {
   stage '\u2776 Checkout'
       checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'poojabansal607@gmail.com', url: 'https://github.com/poojabansal607/test-app.git']]])
       def mvnHome = tool 'M3'
   		//echo 'Hello World 1'
   stage '\u2777 Build'
      
	  // def pom = readMavenPom file: 'pom.xml'
	  // def version = pom.version.replace("-SNAPSHOT", ".${currentBuild.number}")
	   sh "${mvnHome}/bin/mvn clean install"
	  
	 
	 step([$class: 'ArtifactArchiver', artifacts: '**/target/*.jar', fingerprint: true])
	 step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
	 echo "\u2600 BUILD_URL=${env.BUILD_URL}"
	
	 def workspace = pwd()
     echo "\u2600 workspace=${workspace}"
	   // input 'Publish?'
	     // Email for build 
	    emailext body: '''Hi,
		Build is successful.
		Regards,
		Pooja''', compressLog: true, recipientProviders: [[$class: 'DevelopersRecipientProvider']], subject: 'Build is successful', to: 'pbansal13@sapient.com'
   		//echo 'Hello World 2'
		
		 stage 'Deploy to QA'
         puppet.credentials 'secret'
		 puppet.codeDeploy 'production', credentials: 'secret'


    stage 'Deploy to PROD'
    input "Ready to deploy to PROD?"
//	puppet.hiera scope: 'staging', key: 'build-version', value: version
//	puppet.hiera scope: 'staging', key: 'build-path', value: "http://" + hostaddress + "/builds/app/build-${version}.tar.gz"
//  puppet.codeDeploy 'production', credentials: 'SecretID'
   
   
		 
} 