def imageName = 'jfmajer/movies-parser'

node ('workers') {
    stage('Checkout') {
        checkout scm
    }

    def imageTest = docker.build("${imageName}-test", "-f Dockerfile.test .")
        stage('Pre-integration Tests') {
            parallel(
                'Quality Tests': {
                     imageTest.inside{
                         sh 'golint'
                         }
                    },
                'List Files': {                
                     imageTest.inside{
                        sh 'ls -la'
                        }
                    },
                'Security Tests': {            
                    imageTest.inside('-u root:root') {
                        sh 'nancy --version'
                         }
                    }
                    )
        }
    stage('Build') {
        docker.build(imageName)
    }
}

