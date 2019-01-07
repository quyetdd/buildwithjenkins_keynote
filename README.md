# buildwithjenkins_keynote
example with heroku 
please login before run script heroku cli
#!/bin/bash -l

export LANG=en_US.UTF-8
heroku git:remote -a wbmedicsmartphone-neos-2
git push heroku +HEAD:master
sonar-scanner \
  -Dsonar.projectKey=wellbe \
  -Dsonar.sources=module/ \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=925e45b0170ae2b33a993c796b4a7c6e809b1b62
  example with android
  #!/bin/bash -l

export LANG=en_US.UTF-8
export ANDROID_HOME=/Users/neos/Library/Android/sdk
  sed -i -e 's/int VERSION = 2/int VERSION = 2/g' app/src/main/java/com/wellbemedic/wellbe/CommonUtil.java #change version client
  #sed -i -e 's/int timeInDay =  24*60*60/int timeInDay =  60/g' app/src/main/java/com/wellbemedic/wellbe/service/VerifyMemberService.java #change version client
  #sed -i -e 's/com.wellbe_medic.WellBeMedicalCommunicationServices/com.wellbemedic.wellbe/g' build.gradle #change package
  
  ./gradlew assembleRelease
  
  

  
  
#sonar-scanner \
#  -Dsonar.projectKey=wellbe_android \
#  -Dsonar.sources=app/ \
#  -Dsonar.host.url=http://localhost:9000 \
#  -Dsonar.java.binaries=app/build/intermediates/javac/release/compileReleaseJavaWithJavac/classes/com/wellbemedic/wellbe/ \
#  -Dsonar.login=6ee6aa9fff8a3af0cb824ed3bddca4d267408a0d
  
   #./gradlew assembleDebug
#sonar-scanner \
#  -Dsonar.projectKey=wellbe_android \
#  -Dsonar.sources=app/ \
#  -Dsonar.host.url=http://localhost:9000 \
#  -Dsonar.java.binaries=app/build/intermediates/javac/debug/compileDebugJavaWithJavac/classes/com/wellbemedic/wellbe/ \
#  -Dsonar.login=6ee6aa9fff8a3af0cb824ed3bddca4d267408a0d

   #upload to deploy gate
   #dgate push Wellbe.apk -m "${GIT_COMMIT}"
   
   #!/bin/bash -l
export LANG=en_US.UTF-8
set +e
sonar-scanner \
  -Dsonar.projectKey=wellbe_android \
  -Dsonar.sources=app/src/main/java/com/wellbemedic/wellbe/ \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.java.binaries=app/build/intermediates/javac/release/compileReleaseJavaWithJavac/classes/com/wellbemedic/wellbe/
  -Dsonar.login=925e45b0170ae2b33a993c796b4a7c6e809b1b62
set -e

Example with ios 
#!/bin/bash -l

export LANG=en_US.UTF-8
xcodebuild -list -workspace WellBe.xcworkspace #list all schema
#need unlock keychain
security unlock -p 11111111 /Users/neos/Library/Keychains/login.keychain-db
pod install
./build.sh
#export file archive 
#xcodebuild -workspace WellBe.xcworkspace -scheme WellBe -destination generic/platform=iOS build archive -archivePath build/WellBe.xcarchive
#xcodebuild -workspace WellBe.xcworkspace -scheme WellBe -destination generic/platform=iOS build archive -archivePath build/WellBe.xcarchive PRODUCT_BUNDLE_IDENTIFIER="neoscorp.vn.technicaldemo"  PROVISIONING_PROFILE_SPECIFIER="technicalDemoProfile" CODE_SIGN_IDENTITY="iPhone Developer: Minh Nguyen Quang (978Q2BK8LZ)"
#xcodebuild -workspace WellBe.xcworkspace -scheme WellBe -sdk iphoneos -configuration AppStoreDistribution archive -archivePath build/WellBe.xcarchive

#export file ipa   
#xcodebuild -exportArchive -archivePath build/WellBe.xcarchive -exportOptionsPlist exportOptions.plist -exportPath build

#Applications/Xcode.app/Contents/Applications/Application\ Loader.app/Contents/Frameworks/ITunesSoftwareService.framework/Support/altool

#upload to itunes connect and using for testflight
#altool --upload-app -f "WellBe.ipa" -u $USERNAME -p $PASSWORD

#upload to deploydate
dgate push $WORKSPACE/build/WellBe.ipa -m "${GIT_COMMIT}"
curl -X POST -H 'Content-type: application/json' --data '{"text":":thumbsup: IOS build R2 - http://localhost:8080/job/IOS_WellBe/changes go to https://deploygate.com to download app"}' https://hooks.slack.com/services/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

