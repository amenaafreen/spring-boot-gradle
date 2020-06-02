// def label = "jenkinsagent-${UUID.randomUUID().toString()}"


podTemplate(containers: [
                containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
                containerTemplate(name: 'java', image: 'openjdk:8-jdk', command: 'cat', ttyEnabled: true,),
   ],
            volumes: [
                persistentVolumeClaim(mountPath: '/root/.gradle/caches', claimName: 'pvc', readOnly: false),
  ]
  ) {

  node(POD_LABEL) {
    stage('Build a Gradle Project') {
      git 'https://github.com/amenaafreen/spring-boot-gradle.git'
      container('java') {
          sh './gradlew -g $PWD clean build'
      }
    }
  }
}
