# 1.查看docker服务机器IP,然后在broker.p中设置
# 2.修改kitematic中映射的docker外部端口 10911:10911   9876:9876  端口相互对应, 
# 3.报10909端口链接错误时,对应的生产者和消费者 设置 vip通道关闭   producer.setVipChannelEnabled(false);

FROM  maven:3.3.1

RUN groupadd admin && useradd -g admin -s /bin/bash -c Admin admin  && mkdir -p /home/admin && chown admin /home/admin
USER admin
RUN cd /home/admin && git clone https://github.com/wangyumi/RocketMQ.git
WORKDIR /home/admin/RocketMQ
RUN mvn -Dmaven.test.skip=true clean package install assembly:assembly -U
RUN ln -s target/alibaba-rocketmq-3.2.6-alibaba-rocketmq/alibaba-rocketmq devenv

ENV JAVA_HOME=/usr/lib/jvm/java-1.7.0-openjdk-amd64


WORKDIR /home/admin/RocketMQ/devenv/bin
RUN wget https://kinglf.github.io/docker/rocketmq/broker.p
RUN rm play.sh
RUN wget https://kinglf.github.io/docker/rocketmq/play.sh
EXPOSE 10911
EXPOSE 9876
CMD  ["sh", "-c", ". ./play.sh; while sleep 10; do echo RocketMQ, GO ROCK; done"]
