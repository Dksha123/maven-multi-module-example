pipeline{

agent any
 options {

             skipDefaultCheckout true
 }
stages{

stage('SCM'){

steps{

    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/samridhi97/maven-multi-module-example.git']]])

} }

stage('BUILD'){

steps{

sh '/opt/maven/bin/mvn clean package -Dmaven.test.skip=true'

}
}

stage('RELEASE') {

steps{

sh '/opt/maven/bin/mvn --batch-mode release:clean release:prepare release:perform -DreleaseVersion=5.1 -DdevelopmentVersion=2.4-SNAPSHOT'

}
    
}
stage('GIT PUSH') {
    steps{
    
        sh 'git push https://samridhi97:github97@github.com/samridhi97/maven-multi-module-example.git HEAD:master'

}
}
}
 }

