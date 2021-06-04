def artifactFile = ''

def PROJECT_NAME = "test"

pipeline {
    agent any

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        script {

            sh """
                    xcodebuild archive \
                    -scheme test \
                    -archivePath ./build/test-iphonesimulator.xcarchive \
                    -sdk iphonesimulator \
                    SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES


                    xcodebuild archive \
                    -scheme test \
                    -archivePath ./build/test-iphoneos.xcarchive \
                    -sdk iphoneos \
                    SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES

                    xcodebuild -create-xcframework \
                    -framework ./build/test-iphonesimulator.xcarchive/Products/Library/Frameworks/test.framework \
                    -framework ./build/test-iphoneos.xcarchive/Products/Library/Frameworks/test.framework \
                    -output ./build/test.xcframework
                """

        }
    }

    stage('Archive') {
        archiveArtifacts "./build/test.xcframework"
    }
}

