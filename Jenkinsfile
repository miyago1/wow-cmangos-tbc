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
                    rm -rf build && mkdir build
                    cd build
                    cmake -G Ninja ../mangos-tbc -DCMAKE_INSTALL_PREFIX=$WORKSPACE/run -DBUILD_EXTRACTORS=ON -DPCH=1 -DDEBUG=0 -DBUILD_PLAYERBOTS=ON
                    cmake --build . --target install -- -j$(nproc)
                '''
                dir("${WORKSPACE}/run/etc") {
                    sh '''
                        cp -v mangosd.conf.dist mangosd.conf
                        cp -v realmd.conf.dist realmd.conf
                        cp -v anticheat.conf.dist anticheat.conf
                    '''
                }
                sh 'cp -vr "$WORKSPACE/run" "/mnt/lxc-shared/wow/builds/cmangos-tbc/$BUILD_NUMBER"'
            }
        }
    }
}