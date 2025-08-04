pipeline {
    agent {
        label 'wow-compile1'  
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello, World!'
                dir('mangos-tbc') {
                    git branch: 'master', url: 'https://github.com/cmangos/mangos-tbc.git'
                }
                sh '''
                    mkdir -p build
                    cd build
                    cmake ../mangos-tbc -DCMAKE_INSTALL_PREFIX=$WORKSPACE/run -DBUILD_EXTRACTORS=ON -DPCH=1 -DDEBUG=0 -DBUILD_PLAYERBOTS=ON
                    ls $WORKSPACE/run
                '''
            }
        }
    }
}