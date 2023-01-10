# About-the-xml-file-import-target（idea）
问题：mapper层中设置了xml文件，但是在项目中target没有加载出来。（这些xml文件：在更复杂的持久层程序时，需要这些xml文件来进行配置）
原因：默认下maven工具针对我们的java目录下的非java文件，不会执行编译操作，所以target文件下是没有xml文件的。

解决方法：
（1）在pom.xml添加bo节点
 <!--项目打包时会将java目录中的*.xml文件也进行打包-->
<resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
 </resources>
 （2）还需要让运行环境找到这个xml文件
 在运行环境yml文件添加
mybatis-plus:
  configuration: #sql日志
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  
  mapper-locations: classpath:com/atguigu/payment/mapper/xml/*.xml
 
 
 
 然后保险起见需要删除target文件重新加载出来新的target文件
 步骤：
 在idea的右侧界面maven中点开生命周期，点击clean进行清除原来的target文件，最后在idea最上侧的功能栏点击（小锤子）重构键进行重新加载target文件。
 
