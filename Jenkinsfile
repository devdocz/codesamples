def myCheckout(myGitUrl, myBranch, myLocalDir) {
    checkout changelog: false, poll: false, scm: [$class: 'GitSCM', 
    branches: [[name: myBranch]], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [[$class: 'RelativeTargetDirectory',
    relativeTargetDir: myLocalDir]], 
    submoduleCfg: [], 
    userRemoteConfigs: [[credentialsId: 'GitHubSSH-10-24',   
    url: myGitUrl]]
    ]
}

node () { 
    stage ('Clone Git') {
        echo 'Cloning Git... devdocz/codesamples'
        def parthak8_url = "git@github.com:devdocz/codesamples.git"
        def parthak8_branch = "*/jenkins-10-24"
        def local_dir = "devdocz"
        myCheckout(parthak8_url, parthak8_branch, local_dir)

        // set an environment variable, value of local_dir
        env.LOCAL_DIR = local_dir 

        sh "ls -la"
        sh "ls -la ${LOCAL_DIR}"
        def CWDABSPATH
        CWDABSPATH = sh (
        script: "echo `pwd`",
                returnStdout: true
        ).trim()
        println "Current Working Directory: " + CWDABSPATH
        env.BASEPATH = CWDABSPATH  // set env var for BASEPATH
    }

    stage ('Compile using gradle') {
        echo "Starting compilation"

    }

    stage ('Run Unit-tests') {
        echo "Running Unit-tests"

    }

    stage ('Call python script') {
        sh '''#!/bin/bash -l
                python azure_vm_explore.py
        '''
    }

}
