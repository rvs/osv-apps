VERSION:=1.0.0-incubating-SNAPSHOT
NAME:=apache-geode
DIR:=$(NAME)-$(VERSION)
TARBALL:=$(DIR).tar.gz
URL:=https://builds.apache.org/job/Geode-nightly/lastSuccessfulBuild/artifact/gemfire-assembly/build/distributions/$(TARBALL)


module: ROOTFS usr.manifest

$(TARBALL):
	wget $(URL)

ROOTFS/tmp:
	mkdir -p ROOTFS/tmp/$(NAME)
	touch ROOTFS/tmp

ROOTFS/$(NAME): $(TARBALL)
	tar xvf $(TARBALL)
	mkdir -p ROOTFS
	mv $(DIR) ROOTFS/$(NAME)
	touch ROOTFS/$(NAME)
	(cd ./assets ; tar cf - .) | (cd ROOTFS ; tar xf -)
#	find ./assets/ -type f -exec cp {} ROOTFS/$(NAME)/config/. \;

usr.manifest:
	echo "/$(NAME)/**: \$${MODULE_DIR}/ROOTFS/$(NAME)/**" > usr.manifest

clean:
	rm -rf ROOTFS $(DIR)
	rm -f usr.manifest $(TARBALL)

ROOTFS: ROOTFS/$(NAME) ROOTFS/tmp
