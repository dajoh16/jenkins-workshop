node {
    stage("Preparation"){
    checkout scm  
    }
    stage("Build"){
       sh 'docker run -i -v $PWD:/usr/src/mymaven -w /usr/src/mymaven --rm maven:3-jdk-8 mvn clean package'
    }
    stage("Results"){
       junit '**/target/surefire-reports/TEST-*.xml'
       archiveArtifacts artifacts: 'target/gildedrose-*.jar', onlyIfSuccessful: true
    }
    stage("Javadoc")
        echo 'I totally generated some Javadoc'
}