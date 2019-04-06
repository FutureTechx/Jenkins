### CI 
CI：持续集成是一种让计算机自动地任意次重复整个开发流程（编译，测试，汇报等）的开发手法，由于频发重复整个开发流程，所以可以早点发现问题。
### Jenkins 
jenkins是基于java的开源的CI工具，安装和操作很简单，支持插件进行功能扩展，支持主从式聚群。能够轻松的纵向发展。
下面流程是Jenkins实现持续集成的一个例子：
- 为job的执行制定日程表
- 签出源码
- 通过shell脚本进行测试并输出结果
- 通过shell脚本构建文档
- 统计TODO
- 发送邮件通知Job的结果
- 将Job的结果保存到Slack

### jenkins 常用的控件
控件的安装可以通过”系统管理“页面。也可以使用CLI(Command Line Interfac，命令行接口)进行安装，但要先下载CLI工具：
 wget http://localhost:8080/jnlpJars/jenkins-cli.jar
通过CLI工具安装插件
java -jar kenkins-cli.jar -s http://localhost:8080 install-plugin tasks mercurial slack cobertura
重启jenkins,使刚才安装的插件生效
sudo service jenkins restart

整个流程：
- 安装jenkins
- 安装用到的插件
- 添加job
- 指定源代码管理系统
- 制定日程表
- 设置执行测试代码的命令
- 测试结果输出到报告中
使用pytest来输出测试结果的报告
1 安装pytest:pip install pytest
2 调用pytest命令
py.test --junit-xml=test-result.xml
该命令输出一个xUnit格式的test_result.xml文件，现在用jenkins读取它，就能从屏幕中看到测试结果了
- 根据pytest更改Jenkins的设置。
- 显示覆盖率报告
1 安装pytest-cov
2 从pytest获取覆盖率
- 读取覆盖率报告
- 邮件通知
- 向Slack发送通知