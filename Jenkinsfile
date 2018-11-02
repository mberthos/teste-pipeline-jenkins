node ("${params.xenserver_name}"){
   currentBuild.description = "#${BUILD_NUMBER}, ${VM_Name}, ${xenserver_name}, ${IP}"
   echo "Creating a new vm ${vm_name} on ${xenserver_name} with IP ${IP}"

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
         sh "mkdir -p /etc/chef"${xenserver_name}
         //sh "sudo chmod -R +x ${WORKSPACE}//repo//*.*"
   }

   stage ('RUN_SCRIPT_CREATE_VM'){
           sh "sudo /home/marcelo.bertho/./vm-creator.sh  ${VM_Name} ${sr_xenserver_uuid}  ${Template} ${Data_Center} ${IP} wavy true http://mirror-diveo.datac.movile.com/kumo/movile-user-data.sh"

   }

   stage ('CALL_CHEF_PROVISION'){
              //build(job: 'jenkins-test-project-build', param1 : 'some-value')
              //build 'pipeline-local'
              echo "Executing role-base "
   }

   stage ('FINAL_TEST'){
              //build(job: 'jenkins-test-project-build', param1 : 'some-value')
              echo "VM Passed and it is dne to delivery"
      }

}
