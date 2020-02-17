node {



    def isMainline = ["develop", "master"].contains(env.BRANCH_NAME)



    List environment = [

        "GOOGLE_APPLICATION_CREDENTIALS=/home/ubuntu/fqdemo-service-credentials-key.json"

    ]



    stage('Checkout') {

        // Pull the code from the repo

        checkout scm

    }



    stage('Clean') {

        sh "./gradlew clean"

    }



    



    stage 'Build Release'

        sh "./gradlew assembleRelease"





   if (isMainline) {



        stage 'Archive'

             archiveArtifacts artifacts: 'app/build/outputs/apk/release/*.apk', fingerprint: false, allowEmptyArchive: false



          stage ('Distribute') {

              withEnv(environment) {

                  sh "./gradlew assembleRelease appDistributionUploadRelease"

              }

          }



    }



}
