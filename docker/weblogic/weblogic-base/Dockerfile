FROM registry.cn-hangzhou.aliyuncs.com/kennylee/java:centos-serverjre8

MAINTAINER playniuniu <playniuniu@gmail.com>

ENV FMW_PKG=fmw_12.2.1.2.0_wls_quick_Disk1_1of1.zip \
    FMW_JAR=fmw_12.2.1.2.0_wls_quick.jar \
    ORACLE_WEBLOGIC12_URL="http://opbfi59h0.bkt.clouddn.com/fmw_12.2.1.2.0_wls_quick_Disk1_1of1.zip" \
    SCRIPT_FILE=/u01/oracle/createAndStartEmptyDomain.sh \
    ORACLE_HOME=/u01/oracle \
    USER_MEM_ARGS="-Djava.security.egd=file:/dev/./urandom" \
    DEBUG_FLAG=true \
    PRODUCTION_MODE=dev \
    DOMAIN_NAME="${DOMAIN_NAME:-base_domain}" \
    DOMAIN_HOME=/u01/oracle/user_projects/domains/${DOMAIN_NAME:-base_domain} \
    ADMIN_PORT="${ADMIN_PORT:-8001}" \
    PATH=$PATH:/usr/java/default/bin:/u01/oracle/oracle_common/common/bin:/u01/oracle/wlserver/common/bin

COPY weblogic-config/install.file weblogic-config/oraInst.loc /u01/
COPY container-scripts/createAndStartEmptyDomain.sh container-scripts/create-wls-domain.py /u01/oracle/

# add local file for test
# COPY $FMW_PKG /u01/$FMW_PKG

RUN useradd -b /u01 -M -s /bin/bash oracle \
    && echo oracle:oracle | chpasswd \
    && cp /etc/skel/.bash* $ORACLE_HOME \
    && curl -SL ${ORACLE_WEBLOGIC12_URL} -o /u01/$FMW_PKG \
    && chown oracle:oracle -R /u01 \
    && cd /u01 \
    && $JAVA_HOME/bin/jar xf /u01/$FMW_PKG \
    && su - oracle -c "$JAVA_HOME/bin/java -jar /u01/$FMW_JAR -ignoreSysPrereqs -force -novalidation \
    -invPtrLoc /u01/oraInst.loc -jreLoc $JAVA_HOME ORACLE_HOME=$ORACLE_HOME" \
    && rm /u01/$FMW_JAR /u01/$FMW_PKG /u01/oraInst.loc /u01/install.file \
    && chmod +rx $SCRIPT_FILE

WORKDIR ${ORACLE_HOME}

CMD ["/u01/oracle/createAndStartEmptyDomain.sh"]
