FROM ubuntu AS base
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
        wget \
        unzip
RUN wget -O /tmp/terraria-server.zip https://terraria.org/api/download/pc-dedicated-server/terraria-server-1449.zip
RUN unzip /tmp/terraria-server.zip '1449/Linux/*' -d /tmp/terraria-server
RUN cp -r /tmp/terraria-server/1449/Linux/ /opt/terraria
RUN chmod +x /opt/terraria/TerrariaServer /opt/terraria/TerrariaServer.bin.x86_64

FROM ubuntu
COPY --from=base /opt/terraria /opt/terraria
COPY serverconfig.txt /etc/terraria/serverconfig.txt
ENTRYPOINT ["/opt/terraria/TerrariaServer"]
CMD ["-config", "/etc/terraria/serverconfig.txt"]