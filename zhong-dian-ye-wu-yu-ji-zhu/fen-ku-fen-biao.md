mycat 
当出现“ wrapper  | The mycat service is not installed - 指定的服务未安装。 (0x424)”
1.先mycat install
2.再mycat start

假如用mysql客户端登录mycat  mysql -u[test] -p -P8066 
显示错误如下
ERROR 1045 (HY000): Access denied for user '[test]' with host '0:0:0:0:0:0:0:1'

在mycat server.xml 设置防火墙设置如下
<!--这些配置情况下对于127.0.0.1都能以testt账户登录-->
	
	<firewall>
	   <whitehost>
	      <host host="1*7.0.0.*" user="test"/>
	   </whitehost>
       <blacklist check="false">
       </blacklist>
	</firewall>
