// def label = "jenkinsagent-${UUID.randomUUID().toString()}"


podTemplate(containers: [
                containerTemplate(name: 'java', image: 'openjdk:8-jdk', command: 'cat', ttyEnabled: true,),
   ],
            volumes: [
                workspaceVolume(hostPathWorkspaceVolume: '/var/jenkins_home') ]
            
  ) {

  node(POD_LABEL) {
    stage('Build a Gradle Project') {
      git 'https://github.com/amenaafreen/spring-boot-gradle.git'
      container('java') {
          sh './gradlew clean build -g .'
      }
    }
  }
}
