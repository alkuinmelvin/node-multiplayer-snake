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
}
