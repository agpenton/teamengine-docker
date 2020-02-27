FROM tomcat:7.0-jre8

ENV CATALINA_BASE "$CATALINA_HOME"

ENV RES_DIR="/root"
ENV TE_BASE="/root/te_base"

ENV TE_SCRIPTS_DIR="$TE_BASE/scripts" \
    TE_DEPS_DIR="$TE_BASE/resources/lib"

WORKDIR "$RES_DIR"

# add TEAM Engine webapp
ADD teamengine-web-*.war "$RES_DIR/"
RUN unzip -q teamengine-web-*.war -d "$CATALINA_BASE/webapps/teamengine"

# add TEAM Engine common libs
ADD teamengine-web-*-common-libs.zip "$RES_DIR/"
RUN unzip -q teamengine-web-*-common-libs.zip -d "$CATALINA_HOME/lib"

# add TEAM Engine console
ADD teamengine-console-*-base.zip "$RES_DIR/"
RUN unzip -q teamengine-console-*-base.zip -d "$TE_BASE"

# add TEAM Engine binaries
ADD teamengine-console-*-bin.zip "$RES_DIR/"
RUN unzip -o -q teamengine-console-*-bin.zip -d "$TE_BASE"

# set TE_BASE
ENV JAVA_OPTS="-Xms1024m -Xmx2048m -DTE_BASE=$TE_BASE -Djava.awt.headless=true"

# add ETS
ADD ets-*-ctl.zip "$RES_DIR/"
RUN for file in ets-*-ctl.zip; do \
      unzip -q $file -d "$TE_SCRIPTS_DIR"; \
    done

ADD ets-*-deps.zip "$RES_DIR/"
RUN for file in ets-*-deps.zip; do \
      unzip -q -o $file -d "$TE_DEPS_DIR"; \
    done

WORKDIR "$CATALINA_BASE/bin"
CMD ["catalina.sh", "run"]

