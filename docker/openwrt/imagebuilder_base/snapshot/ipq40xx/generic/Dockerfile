
########################################################################
# WARNING: This is an automatically generated Dockerfile. DO NOT EDIT. #
########################################################################

FROM otvorenamreza/firmware-base

RUN mkdir -p /buildsystem/build && \
 chown -R builder:builder /buildsystem/build && \
 sudo -E -u builder ./openwrt/scripts/docker-build snapshot ipq40xx generic && \
 cd /buildsystem/build && \
 mkdir -p /builder/imagebuilder && \
 cp -r imagebuilder/. /builder/imagebuilder && \
 rm -rf imagebuilder && \
 mkdir -p /builder/packages/ && \ 
 echo -n "{\"platform\": \"lede\", " > /builder/packages/metadata && \
 echo -n "\"architecture\": \"ipq40xx_generic\", " >> /builder/packages/metadata && \
 echo -n "\"version\": \"11/20/18 09:31:30\", " >> /builder/packages/metadata && \
 echo -n "\"packages\": " >> /builder/packages/metadata && \
 cd /builder/imagebuilder && \
 make package_index && \
 make package_reload && \
 find /builder/imagebuilder/packages -name Packages | xargs cat | /buildsystem/openwrt/tools/packages2json.py >> /builder/packages/metadata && \
 echo "}" >> /builder/packages/metadata && \
 cp /buildsystem/openwrt/docker/Dockerfile.runtime /builder/Dockerfile && \
 chown -R builder:builder /buildsystem/build && \
 { rm -rf /buildsystem 2>/dev/null || true; }

WORKDIR /builder
CMD tar cvzhf - .
