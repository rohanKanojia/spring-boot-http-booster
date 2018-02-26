podTemplate(name: 'maven33', label: 'maven33', cloud: 'openshift', containers: [
    containerTemplate(name: 'jnlp',
        image: 'openshift/jenkins-slave-maven-centos7',
        workingDir: '/tmp',
        serviceAccount: 'jenkins',
        envVars: [
            envVar(key: 'MAVEN_MIRROR_URL',value: 'http://nexus-myproject.192.168.64.91.nip.io/nexus/content/groups/public/')
        ],
        cmd: '',
        args: '${computer.jnlpmac} ${computer.name}')
]){
  node("maven33") {
    checkout scm
    stage("Test") {
      sh "mvn test"
    }
    stage("Deploy") {
      sh "mvn  -Popenshift -DskipTests clean fabric8:deploy"
    }
  }
}