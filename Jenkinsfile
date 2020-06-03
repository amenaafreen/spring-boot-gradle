// def label = "jenkinsagent-${UUID.randomUUID().toString()}"


podTemplate(containers: [
                containerTemplate(name: 'java', image: 'openjdk:8-jdk', command: 'cat', ttyEnabled: true,),
   ],
             volumes: [
               persistentVolumeClaim(mountPath: "/home/jenkins/workspace/${JOB_NAME}/.gradle/caches", claimName: 'pvc', readOnly: false)
            ]
            ) {

  node(POD_LABEL) {
    stage('Build a Gradle Project') {
      println "Home: ${HOME}"
      println "Workspace: ${WORKSPACE}"
      git 'https://github.com/amenaafreen/spring-boot-gradle.git'
      container('java') {
          sh './gradlew clean build -g /home/jenkins/workspace/${JOB_NAME}/.gradle/caches'
      }
    }
  }
}
