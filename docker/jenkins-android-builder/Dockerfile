FROM jenkins/jnlp-slave:3.23-1

USER root

ENV HOME_PATH=/root
WORKDIR /root
# SDK versions
ENV ANDROID_COMPILE_SDK 28
ENV ANDROID_BUILD_TOOLS 28.0.2
# Set gradle cache directory
ENV GRADLE_USER_HOME=$HOME_PATH/.gradle
# Remove some gradle caches
RUN rm -f  .gradle/caches/modules-2/modules-2.lock
RUN rm -rf .gradle/caches/*/plugin-resolution/
# Install packages
RUN apt-get -qq update --yes && apt-get -qq install --yes wget tar unzip lib32stdc++6 lib32z1 && \
    if [ ! -d android-sdk-linux ]; then wget --quiet --output-document=android-sdk-tools.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip; fi && \
    if [ ! -d android-sdk-linux ]; then unzip -q android-sdk-tools.zip -d android-sdk-linux; fi
# Set path variables
RUN mkdir -p $HOME_PATH/.android && \
    touch $HOME_PATH/.android/repositories.cfg
ENV ANDROID_HOME=$HOME_PATH/android-sdk-linux
ENV PATH=$PATH:$HOME_PATH/android-sdk-linux/platform-tools/
# Install packages
RUN echo y | android-sdk-linux/tools/bin/sdkmanager "platform-tools" > /dev/null
RUN echo y | android-sdk-linux/tools/bin/sdkmanager "platforms;android-$ANDROID_COMPILE_SDK" > /dev/null
RUN echo y | android-sdk-linux/tools/bin/sdkmanager "build-tools;$ANDROID_BUILD_TOOLS" > /dev/null
# Accept all licenses
RUN echo y | android-sdk-linux/tools/bin/sdkmanager --licenses > /dev/null