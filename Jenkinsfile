node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile /home/kawaiii0_/simple-python-pyinstaller-app/sources/add2vals.py /home/kawaiii0_/simple-python-pyinstaller-app/sources/calc.py'
        }
    }

    stage('Test') {
        docker.image('qnib/pytest').inside {
            sh 'py.test --verbose --junit-xml test-reports/results.xml /home/kawaiii0_/simple-python-pyinstaller-app/sources/test_calc.py'
        }
        post {
            always {
                junit 'test-reports/results.xml'
            }
        }
    }

    stage('Deliver') {
        docker.image('cdrx/pyinstaller-linux:python2').inside {
            sh 'pyinstaller --onefile sources/add2vals.py'
        }
        post {
            success {
                archiveArtifacts 'dist/add2vals'
            }
        }
    }
}
