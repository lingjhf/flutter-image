FROM gradle:jdk17-jammy

ENV FLUTTER_HOME=/opt/flutter
ENV ANDROID_HOME=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
ENV PATH=$PATH:$ANDROID_HOME/platform-tools
ENV PATH=$PATH:$ANDROID_HOME/tools
ENV PATH=$PATH:$FLUTTER_HOME/bin

RUN apt-get update && apt-get -y install xz-utils

RUN echo "Downloading flutter" \
    && wget --no-verbose --output-document=flutter.tar.xz "https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.27.1-stable.tar.xz" \
    && echo "Installing flutter" \
    && tar -xJf flutter.tar.xz -C /opt \
    && git config --global --add safe.directory /opt/flutter

RUN echo "Downloading commandlinetools" \
    && wget --no-verbose --output-document=commandlinetools.zip "https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip" \
    && echo "Installing commandlinetools" \
    && mkdir "${ANDROID_HOME}" \
    && unzip commandlinetools.zip -d "${ANDROID_HOME}/cmdline-tools" \
    && mv "${ANDROID_HOME}/cmdline-tools/cmdline-tools" "${ANDROID_HOME}/cmdline-tools/latest/"


RUN yes | sdkmanager "platform-tools" "tools" "build-tools;30.0.3" "platforms;android-30" && sdkmanager --licenses && flutter doctor --android-licenses
