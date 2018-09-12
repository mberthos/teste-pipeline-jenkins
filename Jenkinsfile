node {
   stage 'CLEAN'
        echo 'Hello World'
   
   stage 'CHECKOUT PROJECT'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'PerBuildTag']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'da5a2d11-fa80-4e5b-8add-a69c704c3b13', url: 'https://github.com/mberthos/teste-pipeline-jenkins.git']]])   
   
   stage "CREATE BUILD OUTPUT"
        // Make the output directory.
        sh "mkdir -p output"
        // Write an useful file, which is needed to be archived.
        writeFile file: "output/usefulfile.txt", text: "This file is useful, need to archive it."
        // Write an useless file, which is not needed to be archived.
        writeFile file: "output/uselessfile.md", text: "This file is useless, no need to archive it."

    stage "ARCHIVE BUILD OUTPUT"
         // Archive the build output artifacts.
         archiveArtifacts artifacts: 'output/*.txt', excludes: 'output/*.md'   
}
