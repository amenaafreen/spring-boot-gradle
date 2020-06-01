def label = "jenkinsagent-${UUID.randomUUID().toString()}"


podTemplate(label: label,
        containers: [
                containerTemplate(name: 'jnlp', image: 'jenkins/jnlp-slave:3.27-1', envVars: [ envVar(key: 'GIT_SSL_NO_VERIFY', value: 'true') ],),
                containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
                containerTemplate(name: 'java', image: 'openjdk:8-jdk', command: 'cat', ttyEnabled: true,),
   ],
         volumes: [
                persistentVolumeClaim(mountPath: '/root/.gradle/caches', claimName: 'pvc', readOnly: false),
  ]) {

  node(label) {
    stage('Build a Gradle Project') {
      git 'https://github.com/amenaafreen/spring-boot-gradle.git'
      container('java') {
          sh './gradlew clean build'
      }
    }
  }
}
