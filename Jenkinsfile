node ("${params.xenserver_name}"){
   currentBuild.description = "#${BUILD_NUMBER}, ${vm_name}, ${xenserver_name}, ${IP}"
   echo "Creating a new vm ${vm_name} on ${xenserver_name} with IP ${IP}"

   stage ('UPDATE_ENVIROMENT'){
         sh "mkdir -p /etc/chef"
         //sh "sudo chmod -R +x ${WORKSPACE}//repo//*.*"
   }

   stage ('RUN_SCRIPT_CREATE_VM'){
           sh "sudo /home/jenkins/./vm-creator.sh  ${vm_Name} ${sr_xenserver_uuid}  ${template} ${data_center} ${IP} wavy true http://mirror-diveo.datac.movile.com/kumo/movile-user-data.sh"
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
