pipeline {
    agent none
    options {
        // 15m quiet period as described at https://jenkins.io/blog/2010/08/11/quiet-period-feature/
        // quietPeriod(900)
        disableConcurrentBuilds()
        timeout(time: 3, unit: 'HOURS')
        timestamps()
    }
    environment {
        CHANNEL = 'dev'
        REFERRAL_API_KEY = credentials('REFERRAL_API_KEY')
        BRAVE_GOOGLE_API_KEY = credentials('npm_config_brave_google_api_key')
        LINT_BRANCH = "PRBUILDER_${JOB_NAME}_${BUILD_ID}"
    }
    stages {
        stage("all") {
            parallel {
                // stage("linux") {
                //     agent { label "linux-ci" }
                //     environment {
                //         GIT_CACHE_PATH = "${HOME}/cache"
                //         SCCACHE_BUCKET = 'sccache-brave-browser-lin'
                //     }
                //     stages {
                //         stage('unlock') {
                //             steps {
                //                 sh "rm -rf ${GIT_CACHE_PATH}/*.lock"
                //             }
                //         }
                //         stage('install') {
                //             steps {
                //                 sh 'npm install'
                //             }
                //         }
                //         stage('init') {
                //             when {
                //                 not {
                //                     expression { return fileExists('src/brave/package.json') }
                //                 }
                //             }
                //             steps {
                //                 sh 'npm run init'
                //             }
                //         }
                //         stage('sync') {
                //             steps {
                //                 sh 'npm run sync --all'
                //             }
                //         }
                //         stage('lint') {
                //             steps {
                //                 // lint requires the code to be on a branch
                //                 // create a temp branch (and cleanup afterwards)
                //                 sh """
                //                     git -C src/brave config user.name brave-builds
                //                     git -C src/brave config user.email devops@brave.com

                //                     git -C src/brave checkout -b ${LINT_BRANCH}

                //                     npm run lint

                //                     git -C src/brave checkout -
                //                     git -C src/brave branch -D ${LINT_BRANCH}
                //                 """
                //             }
                //         }
                //         stage('build') {
                //             steps {
                //                 sh """
                //                     npm config --userconfig=.npmrc set brave_referrals_api_key ${REFERRAL_API_KEY}
                //                     npm config --userconfig=.npmrc set brave_google_api_endpoint https://location.services.mozilla.com/v1/geolocate?key=
                //                     npm config --userconfig=.npmrc set brave_google_api_key ${BRAVE_GOOGLE_API_KEY}
                //                     npm config --userconfig=.npmrc set google_api_endpoint "safebrowsing.brave.com"
                //                     npm config --userconfig=.npmrc set google_api_key "dummytoken"
                //                     npm config --userconfig=.npmrc set sccache "sccache"

                //                     npm run build -- Release --channel=${CHANNEL} --debug_build=false --official_build=true
                //                 """
                //             }
                //         }
                //         stage('test-security') {
                //             steps {
                //                 script {
                //                     try {
                //                         sh 'npm run test-security -- --output_path="src/out/Release/brave"'
                //                     }
                //                     catch (ex) {
                //                         currentBuild.result = 'UNSTABLE'
                //                     }
                //                 }
                //             }
                //         }
                //         stage('test-unit') {
                //             steps {
                //                 script {
                //                     try {
                //                         sh 'npm run test -- brave_unit_tests Release --output brave_unit_tests.xml'
                //                         xunit([GoogleTest(deleteOutputFiles: true, failIfNotNew: true, pattern: 'src/brave_unit_tests.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
                //                     }
                //                     catch (ex) {
                //                         currentBuild.result = 'UNSTABLE'
                //                     }
                //                 }
                //             }
                //         }
                //         stage('test-browser') {
                //             steps {
                //                 script {
                //                     try {
                //                         sh 'npm run test -- brave_browser_tests Release --output brave_browser_tests.xml'
                //                         xunit([GoogleTest(deleteOutputFiles: true, failIfNotNew: true, pattern: 'src/brave_browser_tests.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
                //                     }
                //                     catch (ex) {
                //                         currentBuild.result = 'UNSTABLE'
                //                     }
                //                 }
                //             }
                //         }
                //         stage('dist') {
                //             steps {
                //                 sh "npm run create_dist -- Release --channel=${CHANNEL} --debug_build=false --official_build=true"
                //             }
                //             post {
                //                 always {
                //                     archiveArtifacts artifacts: 'src/out/Release/**/*.deb,src/out/Release/**/*.rpm', fingerprint: true
                //                 }
                //             }
                //         }
                //     }
                // }
                // stage("mac") {
                //     agent { label "mac-ci" }
                //     environment {
                //         GIT_CACHE_PATH = "${HOME}/cache"
                //         SCCACHE_BUCKET = 'sccache-brave-browser-mac'
                //     }
                //     stages {
                //         stage('unlock') {
                //             steps {
                //                 sh "rm -rf ${GIT_CACHE_PATH}/*.lock"
                //             }
                //         }
                //         stage('install') {
                //             steps {
                //                 sh 'npm install'
                //             }
                //         }
                //         stage('init') {
                //             when {
                //                 not {
                //                     expression { return fileExists('src/brave/package.json') }
                //                 }
                //             }
                //             steps {
                //                 sh 'npm run init'
                //             }
                //         }
                //         stage('sync') {
                //             steps {
                //                 sh 'npm run sync --all'
                //             }
                //         }
                //         stage('lint') {
                //             steps {
                //                 sh """
                //                     git -C src/brave config user.name brave-builds
                //                     git -C src/brave config user.email devops@brave.com

                //                     git -C src/brave checkout -b ${LINT_BRANCH}

                //                     npm run lint

                //                     git -C src/brave checkout -
                //                     git -C src/brave branch -D ${LINT_BRANCH}
                //                 """
                //             }
                //         }
                //         stage('build') {
                //             steps {
                //                 sh """
                //                     npm config --userconfig=.npmrc set brave_referrals_api_key ${REFERRAL_API_KEY}
                //                     npm config --userconfig=.npmrc set brave_google_api_endpoint https://location.services.mozilla.com/v1/geolocate?key=
                //                     npm config --userconfig=.npmrc set brave_google_api_key ${BRAVE_GOOGLE_API_KEY}
                //                     npm config --userconfig=.npmrc set google_api_endpoint "safebrowsing.brave.com"
                //                     npm config --userconfig=.npmrc set google_api_key "dummytoken"
                //                     npm config --userconfig=.npmrc set sccache "sccache"

                //                     npm run build -- Release --channel=${CHANNEL} --debug_build=false --official_build=true
                //                 """
                //             }
                //         }
                //         stage('test-security') {
                //             steps {
                //                 script {
                //                     try {
                //                         sh 'npm run test-security -- --output_path="src/out/Release/Brave\\ Browser\\ Dev.app/Contents/MacOS/Brave\\ Browser\\ Dev"'
                //                     }
                //                     catch (ex) {
                //                         currentBuild.result = 'UNSTABLE'
                //                     }
                //                 }
                //             }
                //         }
                //         stage('test-unit') {
                //             steps {
                //                 script {
                //                     try {
                //                         sh 'npm run test -- brave_unit_tests Release --output brave_unit_tests.xml'
                //                     }
                //                     catch (ex) {
                //                         currentBuild.result = 'UNSTABLE'
                //                     }
                //                     xunit([GoogleTest(deleteOutputFiles: true, failIfNotNew: true, pattern: 'src/brave_unit_tests.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
                //                 }
                //             }
                //         }
                //         stage('test-browser') {
                //             steps {
                //                 script {
                //                     try {
                //                         sh 'npm run test -- brave_browser_tests Release --output brave_browser_tests.xml'
                //                         xunit([GoogleTest(deleteOutputFiles: true, failIfNotNew: true, pattern: 'src/brave_browser_tests.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
                //                     }
                //                     catch (ex) {
                //                         currentBuild.result = 'UNSTABLE'
                //                     }
                //                 }
                //             }
                //         }
                //         stage('dist') {
                //             steps {
                //                 sh "npm run create_dist -- Release --channel=${CHANNEL} --debug_build=false --official_build=true --skip_signing"
                //             }
                //             post {
                //                 always {
                //                     archiveArtifacts artifacts: 'src/out/Release/**/*.dmg', fingerprint: true
                //                 }
                //             }
                //         }
                //     }
                // }
                stage("windows-x64") {
                    agent { label "windows-temp" }
                    environment {
                        GIT_CACHE_PATH = "$USERPROFILE\\cache"
                        SCCACHE_BUCKET = 'sccache-brave-browser-win'
                        PATH = "C:\\Program Files (x86)\\Windows Kits\\10\\bin\\10.0.17134.0\\x64\\;C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Community\\Common7\\IDE\\Remote Debugger\\x64;$PATH"
                        SIGNTOOL_ARGS = "sign /t  http://timestamp.verisign.com/scripts/timstamp.dll  /fd sha256 /sm"
                        KEY_CER_PATH = "C:\\jenkins\\digicert-key\\digicert.cer"
                        KEY_PFX_PATH = "C:\\jenkins\\digicert-key\\digicert.pfx"
                        AUTHENTICODE_PASSWORD = credentials('digicert-brave-browser-development-certificate')
                        CERT = "Brave"
                    }
                    stages {
                        stage('unlock') {
                            steps {
                                powershell "Remove-Item ${GIT_CACHE_PATH}\\*.lock"
                            }
                        }
                        stage('install') {
                            steps {
                                powershell 'npm install'
                            }
                        }
                        stage('init') {
                            when {
                                not {
                                    expression { return fileExists('src/brave/package.json') }
                                }
                            }
                            steps {
                                powershell 'npm run init'
                            }
                        }
                        stage('sync') {
                            steps {
                                powershell 'npm run sync --all'
                            }
                        }
                        stage('lint') {
                            steps {
                                powershell """
                                    git -C src/brave config user.name brave-builds
                                    git -C src/brave config user.email devops@brave.com

                                    git -C src/brave checkout -b ${LINT_BRANCH}

                                    npm run lint

                                    git -C src/brave checkout -
                                    git -C src/brave branch -D ${LINT_BRANCH}
                                """
                            }
                        }
                        // stage('build') {
                        //     steps {
                        //         powershell """
                        //             npm config --userconfig=.npmrc set brave_referrals_api_key ${REFERRAL_API_KEY}
                        //             npm config --userconfig=.npmrc set brave_google_api_endpoint https://location.services.mozilla.com/v1/geolocate?key=
                        //             npm config --userconfig=.npmrc set brave_google_api_key ${BRAVE_GOOGLE_API_KEY}
                        //             npm config --userconfig=.npmrc set google_api_endpoint "safebrowsing.brave.com"
                        //             npm config --userconfig=.npmrc set google_api_key "dummytoken"
                        //             # npm config --userconfig=.npmrc set sccache "sccache"

                        //             npm run build -- Release --channel=${CHANNEL} --debug_build=false --official_build=true
                        //         """
                        //     }
                        // }
                        // stage('test-security') {
                        //     steps {
                        //         script {
                        //             try {
                        //                 powershell 'npm run test-security -- --output_path="src/out/Release/brave.exe"'
                        //             }
                        //             catch (ex) {
                        //                 currentBuild.result = 'UNSTABLE'
                        //             }
                        //         }
                        //     }
                        // }
                        // stage('test-unit') {
                        //     steps {
                        //         script {
                        //             try {
                        //                 powershell 'npm run test -- brave_unit_tests Release --output brave_unit_tests.xml'
                        //                 xunit([GoogleTest(deleteOutputFiles: true, failIfNotNew: true, pattern: 'src/brave_unit_tests.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
                        //             }
                        //             catch (ex) {
                        //                 currentBuild.result = 'UNSTABLE'
                        //             }
                        //         }
                        //     }
                        // }
                        // stage('test-browser') {
                        //     steps {
                        //         script {
                        //             try {
                        //                 powershell 'npm run test -- brave_browser_tests Release --output brave_browser_tests.xml'
                        //                 xunit([GoogleTest(deleteOutputFiles: true, failIfNotNew: true, pattern: 'src/brave_browser_tests.xml', skipNoTestFiles: false, stopProcessingIfError: true)])
                        //             }
                        //             catch (ex) {
                        //                 currentBuild.result = 'UNSTABLE'
                        //             }
                        //         }
                        //     }
                        // }
                        stage('dist') {
                            steps {
                                powershell "npm run create_dist -- Release --channel=${CHANNEL} --debug_build=false --official_build=true"
                                powershell '(Get-Content "src\\brave\\vendor\\omaha\\omaha\\hammer-brave.bat") | % { $_ -replace "10.0.15063.0\\", "" } | Set-Content "src\\brave\\vendor\\omaha\\omaha\\hammer-brave.bat"'
                                powershell """
                                    Set-PSDebug -Trace 2
                                    Import-PfxCertificate -FilePath "${KEY_PFX_PATH}" -CertStoreLocation "Cert:\\LocalMachine\\My" -Verbose -Password (ConvertTo-SecureString -String "${AUTHENTICODE_PASSWORD}" -Force -AsPlaintext)

                                    $env:KEY_CER_PATH=$KEY_CER_PATH
                                    $env:KEY_PFX_PATH=$KEY_PFX_PATH
                                    echo "$KEY_CER_PATH"
                                    echo "$env:KEY_CER_PATH"
                                    echo "$KEY_PFX_PATH"
                                    echo "$env:KEY_PFX_PATH"

                                    KEY_CER_PATH=${KEY_CER_PATH} KEY_PFX_PATH=${KEY_PFX_PATH} npm run create_dist -- Release --channel=${CHANNEL} --build_omaha --tag_ap=x64-dev --target_arch=x64 --debug_build=false --official_build=true
                                """
                            }
                            // post {
                            //     always {
                            //         archiveArtifacts artifacts: 'src/out/Release/**/BraveBrowser*.exe,src/out/Release/**/brave_installer*.exe,src/out/Release/**/brave-*-win32-*.zip', fingerprint: true
                            //     }
                            // }
                        }
                    }
                }
            }
        }
    }
}
