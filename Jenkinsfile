pipeline{
    agent any

    stages {

        stage('Getting project from CDCI-Checkpoint') {
            steps{
      			checkout([$class: 'GitSCM', branches: [[name: '*/master']],
			extensions: [],
			userRemoteConfigs: [[url: 'https://github.com/Omar-Bensalah/labphase.git']]])
            }
        }

       //stage('Cleaning the project') {
         //   steps{
           //     	sh 'mvn -B -labphase clean'
            //}
        //}

		//stage('Install Dependencies') {
            //steps {
                // Use Node.js and npm installed on the Jenkins agent
              //  sh 'npm install'
           // }
       // }
		
	//stage('Build Angular App') {
          //  steps {
                // Build the Angular app
            //    sh 'npm run build --prod'
            //}
        //}

        //stage('Artifact Construction') {
          //  steps{
            //    	sh "mvn -B -labphase package "
            //}
        //}

       stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t omarbensalah8/labphasetest .'
      }
    }
       stage('Docker login') {
        agent any
         steps {
          withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh 'docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}'
          }
       }
     }

      stage ('Docker push to hub') {
        agent any
        steps {
          sh 'docker push omarbensalah8/labphasetest:latest'
        }
      }
}
	    
        post {
        success {
            // Define post-build actions, if needed
            // For example, you can archive the build artifacts
            archiveArtifacts(allowEmptyArchive: true, artifacts: 'dist/**')
            //cleanWS()
        }
    }	
}
       
