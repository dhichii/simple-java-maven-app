node {
    withDockerContainer(image: 'maven', args: '-v /root/.m2:/root/.m2') {
        stage('Build') {
            checkout scm
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy? (klik "Proceed" untuk melanjutkan)'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sleep 60
        }
    }
}
