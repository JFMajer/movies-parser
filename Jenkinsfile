def imageName = 'jfmajer/movies-parser'

node ('workers') {
    stage('Checkout') {
        checkout scm
    }

    def imageTest = docker.build("${imageName}-test", "-f Dockerfile.test .")

    stage('Quality tests') {
            imageTest.inside{
                sh 'golint'
            }
    }
    stage('Security Test') {
        imageTest.inside('-u root:root') {
            sh 'nancy /go/src/github/jfmajer/movies-parser/Gopkg.lock'
        }
    }
}
