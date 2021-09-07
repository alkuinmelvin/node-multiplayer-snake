node ('ubuntu-agent'){  
    def app
    stage('Cloning Git') {
       /* Let's make sure we have the repository cloned to our workspace */
       checkout scm   
    }  

   stage('SAST SNYK'){
     snykSecurity(
          failOnIssues: false, 
          snykInstallation: 'Snyk V2', 
          snykTokenId: 'my-snyk-token'
          // place other parameters here, syntax generated using pipeline script generator in Jenkins
     )
    }

    stage("SAST SonarQube Analysis") {
     steps {
          withSonarQubeEnv('SonarQube') {   // name of SonarQube Configuration Installation in Jenkins
          sh "${scannerHome}/bin/sonar-scanner"
      }
     }
    }

    stage("SAST SonarQube Quality gate") {
     steps {
          waitForQualityGate abortPipeline: true
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




