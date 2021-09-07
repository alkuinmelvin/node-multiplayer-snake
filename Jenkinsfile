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

     stage('SonarQube analysis') {
     tools {
          jdk "jdk11" // the name you have given the JDK installation in Global Tool Configuration
     }
     environment {
          scannerHome = tool 'SonarQube-Scanner' // the name you have given the Sonar Scanner (in Global Tool Configuration)
     }
     steps {
          withSonarQubeEnv(installationName: 'SonarQube-Server') {  // name of scanner in Jenkins Global Tool Configuration
               sh "${scannerHome}/bin/sonar-scanner -X"
          }
     }
     }
}
