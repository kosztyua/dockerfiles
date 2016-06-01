FROM node:5.4

MAINTAINER Andras Kosztyu, kosztyua@vipcomputer.hu

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
    apt-get install -yq \
    git

RUN git clone https://github.com/seejohnrun/haste-server.git /app
WORKDIR /app
RUN npm install

ADD ./app.sh /app/
RUN chmod 755 app.sh
ADD ./highlight.min.js /app/static/
ADD ./default.min.css /app/static/
RUN sed -i -e "s/<title>hastebin<\/title>/<title>pentest's pastebin<\/title>/g" /app/static/index.html  
RUN sed -i -e "s/haste('pentest's pastebin'/haste('pentest\\\'s pastebin'/g" /app/static/index.html
RUN sed -i -e "s/solarized_dark.css/default.min.css/g" /app/static/index.html

ADD ./haste-baseurl-patch-generator.pl /app/
RUN perl haste-baseurl-patch-generator.pl bin
RUN patch -p0 < baseurl.patch 

EXPOSE 7777

CMD [ "./app.sh" ]
