# Copyright 2020 Alex Woroschilow (alex.woroschilow@gmail.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
PWD:=$(shell pwd)

all: init clean
	mkdir --parents $(PWD)/build/Boilerplate.AppDir/art
	$(PWD)/bin/Apprepo.AppImage --destination=$(PWD)/build appdir boilerplate libatk1.0-0 libatk-bridge2.0-0 libgtk-3-0 libreadline8 \
										libselinux1 libtinfo6 libncurses6 libtinfo5 libssh-4 libgcrypt20 libsystemd0 libwayland-cursor0 libselinux1 

	wget --output-document="$(PWD)/build/build.tar.xz" https://bitbucket.org/agriggio/art/downloads/ART-1.16.3-linux64.tar.xz
	tar -xf $(PWD)/build/build.tar.xz -C $(PWD)/build

	echo "LD_LIBRARY_PATH=\$${LD_LIBRARY_PATH}:\$${APPDIR}/art"  >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "exec \$${APPDIR}/art/ART \"\$${@}\""                   >> $(PWD)/build/Boilerplate.AppDir/AppRun

	cp --force --recursive $(PWD)/build/ART-*linux64/* $(PWD)/build/Boilerplate.AppDir/art

	rm --force $(PWD)/build/Boilerplate.AppDir/*.png 		|| true
	rm --force $(PWD)/build/Boilerplate.AppDir/*.svg 		|| true
	rm --force $(PWD)/build/Boilerplate.AppDir/*.jpg 		|| true
	rm --force $(PWD)/build/Boilerplate.AppDir/*.desktop 	|| true

	cp --force $(PWD)/AppDir/*.desktop $(PWD)/build/Boilerplate.AppDir/ 	|| true
	cp --force $(PWD)/AppDir/*.png $(PWD)/build/Boilerplate.AppDir/ 		|| true
	cp --force $(PWD)/AppDir/*.jpg $(PWD)/build/Boilerplate.AppDir/ 		|| true	
	cp --force $(PWD)/AppDir/*.svg $(PWD)/build/Boilerplate.AppDir/ 		|| true

	export ARCH=x86_64 && $(PWD)/bin/appimagetool.AppImage $(PWD)/build/Boilerplate.AppDir $(PWD)/ART.AppImage
	chmod +x $(PWD)/ART.AppImage

init:
	mkdir --parents $(PWD)/bin

	wget https://apprepo.de/appimage/download/apprepo \
		--output-document=$(PWD)/bin/Apprepo.AppImage
	chmod +x $(PWD)/bin/Apprepo.AppImage

	wget https://github.com/AppImage/AppImageKit/releases/download/13/appimagetool-x86_64.AppImage \
		--output-document=$(PWD)/bin/appimagetool.AppImage
	chmod +x $(PWD)/bin/appimagetool.AppImage

clean:
	rm -rf $(PWD)/*.AppImage
	rm -rf $(PWD)/bin/*
	rm -rf $(PWD)/build
