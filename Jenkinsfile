pipeline{

agent any
 options {

             skipDefaultCheckout true
stages{

stage('SCM'){

steps{

    checkout([$class: 'GitSCM', branches: [[name: '*/release']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/samridhi97/maven-multi-module-example.git']]])

} }

stage('BUILD'){

steps{

sh '/opt/maven/bin/mvn clean package -Dmaven.test.skip=true'

}}

stage('RELEASE') {

steps{

sh '/opt/maven/bin/mvn --batch-mode release:clean release:prepare release:perform -DreleaseVersion=5.0 -DdevelopmentVersion=2.3-SNAPSHOT'

}
    
}
stage('GIT PUSH') {
    steps{
    sshagent(credentials: ['gits']) {
        sh 'git push https://samridhi97:github97@github.com/samridhi97/maven-multi-module-example.git HEAD:release'
}
}
}
}}
