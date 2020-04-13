//
// Copyright (c) 2019 Intel Corporation
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//      http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
//

@Library("edgex-global-pipelines@experimental") _

pipeline {
    agent { label 'ubuntu18.04-docker-arm64-4c-16g' }
    stages {
        // this one looks like it only is created for ARM
        stage('Snap my ARM') {
            environment {
                ARCH = 'arm64'
            }
            when {
                expression { findFiles(glob: 'snap/snapcraft.yaml').length == 1 }
            }
            steps {
                script {
                    edgex.bannerMessage 'This is a proof of concept for ARM'
                    sh 'echo v1.1.2 > ./VERSION' // this is to mimic the behavior of edgeXBuildCApp
                    edgeXSnap(
                        jobType: edgex.isReleaseStream()
                            ? 'stage' : 'build'
                    )
                }
            }
        }
    }
}