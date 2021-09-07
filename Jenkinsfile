node ('ubuntu-agent'){  
    def app
    stage('Cloning Git') {
       /* Let's make sure we have the repository cloned to our workspace */
       checkout scm   
    }  

 //  stage('SAST SNYK'){
 //    snykSecurity(
 //         failOnIssues: false, 
 //         snykInstallation: 'Snyk V2', 
 //         snykTokenId: 'my-snyk-token'
 //         // place other parameters here, syntax generated using pipeline script generator in Jenkins
 //    )
 //   }

    stage("SAST SonarQube Analysis") {
      def scannerHome = tool 'SonarQube-Scanner';  // name of scanner in Jenkins Global Tool Configuration
      withSonarQubeEnv('SonarQube-Server') {   // name of SonarQube Server in Jenkins Configuration System) {
        sh "${scannerHome}/bin/sonar-scanner"
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




