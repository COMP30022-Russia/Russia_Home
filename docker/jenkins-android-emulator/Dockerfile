FROM ztl8702/jenkins-android-builder

RUN apt-get -qq update && apt-get -qq install --yes libqt5widgets5 libpulse0

# Download system image and create AVD
RUN echo y | android-sdk-linux/tools/bin/sdkmanager "platforms;android-22" > /dev/null
RUN echo y | android-sdk-linux/tools/bin/sdkmanager "system-images;android-22;google_apis;armeabi-v7a" > /dev/null
RUN echo y | android-sdk-linux/tools/bin/sdkmanager "emulator" > /dev/null
RUN echo no | android-sdk-linux/tools/bin/avdmanager create avd -n test -k "system-images;android-22;google_apis;armeabi-v7a" --tag google_apis --abi armeabi-v7a
RUN echo $ANDROID_HOME