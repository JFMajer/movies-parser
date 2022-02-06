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
    stage('list files') {
        imageTest.inside{
            sh 'ls -la'
        }
    }
    stage('Security Test') {
        imageTest.inside('-u root:root') {
            sh 'go list -json -deps | docker run --rm -i sonatypecommunity/nancy:latest sleuth'
        }
    }
}
