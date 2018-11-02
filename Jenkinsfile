node {
   echo "Creating a new vm ${vm_name} on ${xenserver_name} with IP ${ip}"
   //Create parameters
  
   //Escape error job
   stage('Shell') {
        try {
            sh returnStdout: true, script: 'demo.sh'
        }
        catch (exc) {
            echo 'Something failed!'
        }
    }
   
   //parameters
   parameters {
         //booleanParam(defaultValue: true, description: '', name: 'userFlag')
         string(defaultValue: "TEST", description: 'What environment?', name: 'userFlag')
         choice(choices: ['US-EAST-1', 'US-WEST-2'], description: 'What AWS region?', name: 'region')
   }
   
   stage("TESTPARAMETER") {
       echo "flag: ${params.userFlag}"
       echo "region: ${params.region}"
       sh "df -kh"
   }
   

   stage ('UPDATE_ENVIROMENT'){
         sh "mkdir -p /etc/chef"
         //sh "sudo chmod -R +x ${WORKSPACE}//repo//*.*"        
   }

   stage ('RUN_SCRIPT_CREATE_VM'){
           sh "/vm-creator.sh cupertino4 ${params.Disk_ID} ${params.Disk_ID} ${params.Data_Center} ${params.IP} wavy true http://mirror-diveo.datac.movile.com/kumo/movile-user-data.sh"

   }

   stage ('CALL_CHEF_PROVISION'){
              //build(job: 'jenkins-test-project-build', param1 : 'some-value')
              //build 'pipeline-local'
              echo "Executing role-base "
   }

   stage ('FINAL_TEST'){
              //build(job: 'jenkins-test-project-build', param1 : 'some-value')
              echo "VM Passed and it is dne to delivery ${vm_name}.datac.movile.com"
      }

}
