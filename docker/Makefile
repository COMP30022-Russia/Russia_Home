build-all:
	$(MAKE) -C jenkins-android-builder build
	$(MAKE) -C jenkins-android-emulator build

push-all:
	cd jenkins-android-builder && docker push ztl8702/jenkins-android-builder && cd ..
	cd jenkins-android-emulator && docker push ztl8702/jenkins-android-emulator && cd ..