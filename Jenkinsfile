node ('ubuntu-agent'){  
    def app
    stage('Cloning Git') {
       /* Let's make sure we have the repository cloned to our workspace */
       checkout scm   
    }  

   stage('SAST'){
     steps {
        echo 'Testing...'
        snykSecurity(
          snykInstallation: Snyk V2,
          snykTokenId: my-snyk-token,
          // place other parameters here
        )
      }
    }

    stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("alkuinmelvin/snake")
    }

    stage('Post-to-dockerhub') {
     docker.withRegistry('https://registry.hub.docker.com', 'alkuin_docker') {
            app.push("latest")
        			}
         }

    stage('Pull-image-server') {
         sh "sudo docker-compose down"
         sh "sudo docker-compose up -d"	
      }
}




