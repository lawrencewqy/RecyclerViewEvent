// Every jenkins file should start with either a Declarative or Scripted Pipeline entry point.
node('android'){
    //Utilizing a try block so as to make the code cleaner and send slack notification in case of any error
    try {
        // Global variable declaration
        def project = 'jianguodai-android'
        def appName = 'jianguodai'

        // Stage, is to tell the Jenkins that this is the new process/step that needs to be executed
        stage('Checkout') {
            // Pull the code from the repo
            checkout scm
        }

        //stage('Build Image') {
            // Build our docker Image
            //sh("docker build -t ${project} .")
        //}

        stage('Build') {
           // sh("env >> .env")
           // sh("docker run --env-file .env --rm ${project} ./gradlew clean build assembleRelease")
           // sh("rm -rf .env")

            sh("./gradlew clean assembleDebug")
        }

        stage('archive apks'){
            archiveArtifacts(artifacts: 'app/build/outputs/apk/**/*.apk', fingerprint: true, onlyIfSuccessful: true)
        }
    } catch (e) {
        currentBuild.result = "FAILED"
        throw e
      } finally {
    }
}