# -java17-Path
这个能让你在idea的maven项目中，针对resources内文件于idea测试中找不到的优化修复，以及打包成jar后针对素材的地址优化修复；IDEA Maven file/url path repair and jar file/url path repair; better path tool;


目前未能导出jdk8版本
主要目前使用java17版，idea在同项目下不同版本模块导出jar功能暂不清楚

方法：
Path p = new Path(Main.class);
(void) setClass(Class \_class); 不建议使用，用于修改p对象所指定class
(void) setDefaultEncode(String encode); 设置默认字符编码(默认utf-8)，可用于减少不必要代码
(boolean) isJAR(); 返回当前class文件是否于jar内
(String) getDefaultEncode(); 返回你的默认字符编码
(String) getURLPath(String file); 转换成url地址，由file地址转换返回新的可用地址，
    使用方法:java.net.URL(p.getURLPath("./images/xxx.png")); images文件夹放至resources文件夹内
(String) toEncodePath(String source, (可选，不填使用默认)String encode); 地址文字编码转换，# 不再需要try_catch
    使用方法:System.out.println(p.toEncodePath("c:/%67%12/aa.png"));
(String) getRootPath((可选，不填使用默认)String encode); 获取你的项目根目录
(String) getClassPath(Class classFile); 获取class所在位置，精确到xxx.class，如果已打包为jar，则返回为xxx.jar
(String) getClassFolderPath(Class classFile); 获取class所在目录
(byte[]) getUrlData(URL url); 获取url文件数据，url为本地文件

一般想法与教程：
1、__导入图片：
    _Path p = new Path(Main.class);
    BufferedImage bimg = Image.read(new URL(p.getURLPath("./images/xxx.png")));
    ___
2、__获取jar内文件数据：
    _Path p = new Path(Main.class);
    byte[] data = p.getUrlData(new URL(p.getURLPath("./images/xxx.png")));
    ___
3、__创建/解包/释放一些缓存数据：
    _Path p = new Path(Main.class);
    File f = new File(p.getClassFolderPath(Main.class) + "/xxx.png");
    f.createNewFile();
    ___

如有建议/疑问，欢迎留言
