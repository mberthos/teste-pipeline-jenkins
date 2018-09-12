pipeline{

   echo "Building Job at ${workspace}"
   //Create parameters
   if (params.create){
     parameters {
            choice(
                name: 'Nodes',
                choices:"Linux\nMac",
                description: "Choose Node!")
            choice(
                name: 'Versions',
                choices:"3.4\n4.4",
                description: "Build for which version?" )
            string(
                name: 'Path',
                defaultValue:"/home/pencillr/builds/",
                description: "Where to put the build!")
      }
   }  
       
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
   }
   
   //Stages
   stage ('CLEAN'){
          echo 'Hello World'
          sh "df -kh"      
   }
    
   stage ('UPDATE ENVIROMENT'){
         sh "sudo mkdir -p ${WORKSPACE}//repo"
         //sh "sudo chmod -R +x ${WORKSPACE}//repo//*.*"        
   }
   
   stage ('CHECKOUT PROJECT'){
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'PerBuildTag']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'da5a2d11-fa80-4e5b-8add-a69c704c3b13', url: 'https://github.com/mberthos/teste-pipeline-jenkins.git']]])   
   }
      timeout(time: 60, unit: 'SECONDS') {
         withEnv(["BRANCH=${params.BRANCH}"]) {
               stage "CREATE BUILD OUTPUT"
                   sh "echo $BRANCH"
                   // Make the output directory.
                   sh "mkdir -p output"
                   sleep 5 
                   // Write an useful file, which is needed to be archived.
                   writeFile file: "output/usefulfile.txt", text: "This file is useful, need to archive it."
                   // Write an useless file, which is not needed to be archived.
                   writeFile file: "output/uselessfile.md", text: "This file is useless, no need to archive it."
         }
    }
   
   stage ("ARCHIVE BUILD OUTPUT"){
         // Archive the build output artifacts.
         archiveArtifacts artifacts: 'output/*.txt', excludes: 'output/*.md'   
   }
   
   if(params.calljob){  
     stage ('CALL JOB'){
        //build(job: 'jenkins-test-project-build', param1 : 'some-value')
        build 'pipeline-local' 
      }
   }       

post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }         
}
