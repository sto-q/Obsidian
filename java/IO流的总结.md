 File：
```
  import Java.io.File;
```
 我认为File就像一个对象
```
File a=new File("c://a//b//c.txt")
//那么a就是表示c.txt这个文件，系统无法直接访问c.txt所以要带上路径(相对or绝对)
File parent = new File("F:\\a\\b");

File file3 = new File(parent, "c.txt");

File a=new File("F:\\a\\b");
File b=new File("c.txt");
File file4=new File(a,b);
这是创建File的三个方法
```
 然后就是File的基本方法
 ```
 File a=new File("c://a//b//c.txt")
 String S=a.getAbsolutePath();获取文件绝对路径
 String S=a.getName();获取文件名字
 String S=a.getPath();获取文件路径
 long S=a.length()获取文件大小
 File S=a.getparentFile();获取父级对象("c://a//b")
 File S=a.getparent();获取父级路径
 long s=a.lastModified();获取文件最后修改时间
 long time=System.currentTimeMillis();获取当前时间(毫秒级)
 boolean F=file.canRead();是否可读
 boolean F=file.canWrite();是否可写
 boolean F=file.exists();是否存在
 boolean F=file.isDirectory()是否存在目录-就是文件夹
 boolean F=file.isFile();是否为正常文件
 boolean F=file.isHidden();是否为隐藏文件
 boolean F=file.canExecute();是否可执行
 boolean F=file.createNewFile()throws IOException;创建文件失败抛出IO异常
 boolean F=file.delete();删除文件也可以是文件夹
 boolean F=file.mkdir(mkdirs)创建目录or多级目录
 boolean F=file.renameTo(File name);重命名文件
 前面的boolean F是方便判断是true还是false
 可以直接调用后面的方法
```
```
File[] file=listFiles();列出文件夹下所有文件不包括文件夹
File[] file=listFiles(FileFilter fileter);列出符合条件的文件
例如：FileFilter fileter=new fileFilter(){
//会进行accept方法重写
@Override
public boolean accept(File file){
String name=file.getName();
return name.endswith(".txt")
//返回名字最后为txt的文件
reutn name.startswith("a");
//返回名字前面为a的文件
}
}
File[] file1=file.listFiles()//file1中有file中所有文件
File[] file2=file.listFiles(fileter)//file2中只有文件名最后为txt的文件

```
==接下来是字节流和字符流==
区别：
字节流主要是基本数据类型的，不涉及编码转换，直接读写原始字节，底层机制：二进制
字符流主要是文本数据，**自动处理编码**（如 UTF-8、GBK）底层机制：文本
**字节流**：
File a= new File("");
OutputStream os=new FileOutStream(File file,true)//这个会抛出异常
File也可以换成字符串类型
FileNotFoundException，true表示不覆盖之前的内容，可不填，默认false。
String aa="";
os.write(aa);
os.write(aa,3,aa.length-3)/偏移位置
这个会抛出异常IoException
一口气输入整个字符串
/---------
byet[] byets=aa.getByet();
for(byet b:byets){
os.write(b);
一个字节一个字节的输入
}/-------------
os.flush();这个会抛出异常IoException,将通道内容强制写出。
os.close();这个会抛出异常IoException，关闭通道。
InputStream aa=new InputStream(File file);这个会抛出异常FileNotFoundException;

int length=aa.available();//获取通道中的数据长度
%% %% %% %% %% 
byet byets=new byet[length];
int index=0;
while(true){
byet b=(byet)aa.read(length);
if(b==-1)break;
byets[index++]=b;
 %% %% %% %% %%//一个字节一个的输入
int readcount=aa.read(byets);
将aa内容赋值到byets，readcount获得总共有多少字节.
aa.close(); 关闭通道。
}
现实中应该使用分批处理
byte[] buffer = new byte[1024];
int offset = 0;
while (true){ 
is.read(buffer,offset,40);
if(len == -1) break;
offset += len;
}
Byte streams should only be used for the most primitive I/O.
字节流仅仅适用于读取原始数据（基本数据类型）
**字符流**
//Writer类实现了AutoCloseable接口，因此可以将Writer类对象的构建方法try后面的()中
Writer a=new FileWriter(File file,false).依旧抛出IoException。
String b="----";
%% %% %% 
char[] c=a.toCharArray();
for(char C:c){
a.write(C);
}//一个输入
 %% %% %%
 a.write(c);
 a.write(c,3,c.length-3);
 a.write(b);
 a.flush();强制写入
 /-------------
 Read a=new FileReader(File file);
%% %% %% 
 StringBuilder bu=new StringBuilder();
 while(true){
 int c=a.read();
 if(c==-1)break;
 bu.append(char(c));
 }运用StringBuilder存储在bu中 
 %% %% %%
 char[] aa=new char[1024];
 int count=0;
 while(true){
 // int len=a.read(aa)//一次读取
 int len=a.read(aa,count,50)//一次读取50个
 if(len==-1)break;
 count+=len;
 }

**缓冲流**
try(InputStream is = new FileInputStream(sourceFile);
BufferedInputStream bis = new BufferedInputStream(is);

OutputStream os = new FileOutputStream(destFile);
BufferedOutputStream bos = new BufferedOutputStream(os))
