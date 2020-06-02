// def label = "jenkinsagent-${UUID.randomUUID().toString()}"


podTemplate(containers: [
                containerTemplate(name: 'java', image: 'openjdk:8-jdk', command: 'cat', ttyEnabled: true,),
   ],
             volumes: [
               persistentVolumeClaim(mountPath: '/home/jenkins', claimName: 'pvc', readOnly: false)
            ]
            ) {

  node(POD_LABEL) {
    stage('Build a Gradle Project') {
      git 'https://github.com/amenaafreen/spring-boot-gradle.git'
      container('java') {
          sh 'sleep 10000 && ./gradlew clean build -g .'
      }
    }
  }
}
