FROM buildpack-deps:jessie


ARG LUA_MAKE_MYCFLAGS=""
ARG LUA_MAKE_CC=""


ENV LUA_VERSION 5.3.4
ENV LUA_DOWNLOAD_SHA256 f681aa518233bc407e23acf0f5887c884f17436f000d453b2491a9f11a52400c


RUN set -ex \
  \
  && wget -O lua.tar.gz "https://www.lua.org/ftp/lua-${LUA_VERSION}.tar.gz" \
  && echo "$LUA_DOWNLOAD_SHA256 *lua.tar.gz" | sha256sum -c - \
  \
  && mkdir -p /usr/src/lua \
  && tar -xzf lua.tar.gz -C /usr/src/lua --strip-components=1 \
  && rm lua.tar.gz \
  \
  && cd /usr/src/lua \
  \
  && make linux test \
  && make linux install MYCFLAGS="${LUA_MAKE_MYCFLAGS}" CC="${LUA_MAKE_CC}" \
  \
  && rm -r /usr/src/lua


CMD [ "lua" ]
