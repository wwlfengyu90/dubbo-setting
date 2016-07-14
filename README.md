<h2>##Linux install dubbo</h2>
<h4>
  1.下载Linux版本的Jdk,后缀.tar.gz;<br/>
&nbsp;&nbsp;##下载地址:http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)<br/><br/>
  
  2.配置jdk：<br/>
  &nbsp;&nbsp;##编辑文件:vi /etc/profile,在文件最末,加入如下配置：<br/>
  &nbsp;&nbsp;
  <ul>
	&nbsp;&nbsp;&nbsp;&nbsp;<li>export JAVA_HOME=/opt/jdk1.8.0_92</li>
	&nbsp;&nbsp;&nbsp;&nbsp;<li>export PATH=$JAVA_HOME/bin:$PATH</li>
	&nbsp;&nbsp;&nbsp;&nbsp;<li>export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar</li>
  <ul><br/>
  3.install tomcat <br/>
  &nbsp;&nbsp;##下载地址:http://tomcat.apache.org/<br/><br/>
	
	4.install zookeeper消息中心(依赖jdk)<br/>
	<ul>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
	</ul>
	&nbsp;&nbsp;##下载与安装处理(默认端口1281)：<br/><br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;下载地址: http://www.apache.org/dist//zookeeper/zookeeper-3.4.8/zookeeper-3.4.8.tar.gz<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;解压: tar zxvf zookeeper-3.4.8.tar.gz <br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;将zookeeper-3.4.8/conf里,cp zoo_sample.cfg zoo.cfg ,设置zoo.cfg为默认配置文件<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;执行zookper-3.3.6/bin下./zkServer.sh start,启动zookeeper<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**可以查看java进程/使用netstat -lpn | grep 2181** <br/>
	<br/><br/>
	
	5.get dubbo-admin.war <br/>
	&nbsp;&nbsp;##通过github整个项目工程,打包获得war(github工程地址：https://github.com/alibaba/dubbo):<br/><br/>
	&nbsp;&nbsp;&nbsp;&nbsp;将工程通过maven指令mvn install -DskipTests=true,进行打包 <br/>
	&nbsp;&nbsp;&nbsp;&nbsp;在工程dubbo-admin/target/下会生成dubbo-admin-?.war <br/>
	&nbsp;&nbsp;&nbsp;&nbsp;解压war:将war上传到服务器,先mkdir dubbo-admin,然后在目录里解压war(jar xvf dubbo-admin-?.war)<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;修改dubbo-admin的WEB-INF下的dubbo.properties文件<br/><br/>
	
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dubbo.registry.address=zookeeper://192.168.20.129:2181<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dubbo.admin.root.password=root<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dubbo.admin.guest.password=guest<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;====>具体可以参照,github工程地址内的详细介绍<====<br/><br/>
	
	6.部署项目(可以直接放在tomcat的webapp下面运行)<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;配置tomcat的conf/service.xml<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;在HOST标签内添加Context标签,设置docBase="/*/dubbo-admin" path=""<br/>
	&nbsp;&nbsp;&nbsp;&nbsp;启动tomcat,http://ip:8080/<br/><br/>
</h4>
<h3>##====>通过以上步骤,dubbo管理后台与注册中心zookeeper就配置完成<====##</h3>
