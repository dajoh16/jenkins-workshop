node {
    stage("Preparation"){
     checkout(
            [$class: 'GitSCM', 
            branches: [[name: '*/ready/**']], 
            doGenerateSubmoduleConfigurations: false, 
            extensions: [[$class: 'CleanBeforeCheckout'], 
            pretestedIntegration(gitIntegrationStrategy: squash(), 
            integrationBranch: 'master', 
            repoName: 'jenkins-workshop')], 
            submoduleCfg: [], 
            userRemoteConfigs: [[credentialsId: 'dajoh16', //remember to change credentials and url.
            url: 'git@github.com:dajoh16/jenkins-workshop.git']]])
    }
    stage("Build"){
       sh 'docker run -i -v $PWD:/usr/src/mymaven -w /usr/src/mymaven --rm maven:3-jdk-8 mvn clean package'
    }
    stage("Results"){
       junit '**/target/surefire-reports/TEST-*.xml'
       archiveArtifacts artifacts: 'target/gildedrose-*.jar', onlyIfSuccessful: true
    }
    stage("Publish"){
       pretestedIntegrationPublisher()
    }
    stage("Javadoc")
        echo 'I totally generated some Javadoc'
}