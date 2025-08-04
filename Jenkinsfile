pipeline {
    agent {
        label 'wow-compile1'  
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello, World!'
                git url: 'https://github.com/cmangos/mangos-tbc.git', branch: 'main'
                sh '''
                    mkdir build
                    cd build
                    cmake ../mangos -DCMAKE_INSTALL_PREFIX=$WORKSPACE/run -DBUILD_EXTRACTORS=ON -DPCH=1 -DDEBUG=0 -DBUILD_PLAYERBOTS=ON
                '''
            }
        }
    }
}