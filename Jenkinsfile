def imageName = 'jfmajer/movies-parser'

node ('workers') {
    stage('Checkout') {
        checkout scm
    }
    stage('Quality tests') {
        def imageTest = docker.build("${imageName}-test", "-f Dockerfile.test .")
            imageTest.inside{
                sh 'golint'
            }
    }
}
