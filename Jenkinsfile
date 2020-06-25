node ('ubuntu-slave'){  
    def app
    stage('Cloning Git') {
       checkout scm
    }  
    
 stage('Build') {
       app = docker.build("mikebroomfield/snake")
   }
    
    stage('Push') {
     docker.withRegistry('https://registry.hub.docker.com', 'docker-creds') {
            app.push("latest")
        			}
         }

  
    
    stage('Qualys Scan') {
        
        qualysWASScan authRecord: 'none', cancelOptions: 'none', credsId: '76be5803-d4a8-4f0d-b1de-c07e18d3959d', optionProfile: 'useDefault', platform: 'EU_PLATFORM_1', pollingInterval: '5', scanName: 'mike-test-scan', scanType: 'DISCOVERY', vulnsTimeout: '60*24', webAppId: '9430935'
        
        }
    
    
    stage('Pull') {
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }

}
