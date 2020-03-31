week6课堂作业.md

一、常用JDBC API

在java.sql包中包含体现JDBC基本功能的若干接口和类：

1.Driver 接口：代表驱动程序

2.DriverManager 类：驱动程序管理员

3.Connection 接口：代表数据库连接

4.Statement 、PreparedStatement、CallableStatement 接口：代表数据库操作对象

5.ResultSet 接口：代表结果集

6.DatabaseMetadata、ResultSetMetadata接口：代表元数据

7.Types 类：代表JDBC类型

===============================================================================



二、若干API的具体说明

Statement和 PreparedStatement ------SQL语句执行接口

      Statement 接口代表了一个数据库的状态，再向数据库发送相应的SQL语句时，都需要创建Statement 接口或者PreparedStatement 接口。

Statement 主要用于操作不带参数的SQL语句，比如增、删、改。

PreparedStatement：预编译的Statement接口

     第一步：通过连接获得PreparedStatement 接口对象，用带占位符（？）的sql语句构造。

                    PreparedStatement ps=con.praperedStatement("select * from test where id=?");

    第二步：设置参数

                    ps.setString(1,"5");

    第三步：执行sql语句

                    rs= ps.executeQuery();



Statement 发送完整的sql语句到数据库不是直接执行，而是先编译、后运行。

PreparedStatement 先发送带参数的sql语句，在发送一组参数值。

如果是同构的sql语句，则PreparedStatement 效率高。对于异构的sql语句，两者效率差不多。

同构： 两个sql语句可编译的部分是相同的，只有参数值不同。

异构： 两个sql语句的格式是不同的。

注意点：1.使用预编译的Statement （即PreparedStatement ）编译多条sql语句一起执行。

          2.可以跨数据库使用，编写通用程序。

          3.能用预编译时尽量用预编译。

--------------------------------------------------------------------------------------------------------



ResultSet接口：

     ResultSet接口是查询结果集接口，它对返回的结果集进行处理。ResultSet是程序员进行JDBC操作的必须接口。

---------------------------------------------------------------------------------------------------------



ResultSetMetaData----元数据操作接口：

      ResultSetMetaData 是对元数据进行操作的接口，可以实现很多高级功能。Hibernate运行数据库的操作，大多是通过此接口。可以认为，此接口是SQL查询语言的一种反射机制。ResultSetMetaData 可以通过数据的形式，来遍历数据库各个字段的属性。对于开发者来说，此机制意义重大。

    JDBC通过元数据（MetaData）来获取具体的表相关的信息，例如，可以查询数据库中有哪些表、标有哪些字段、字段的属性等。MetaData 通过一系列的getXXX 将这些信息返回给我们。

    MetaData元数据包括 数据库源数据DatabaseMetadata 和 结果集元数据ResultSetMetaData 。

     数据库源数据DatabaseMetadata： 使用connection.getMetaData()获得了关于数据库整体的元数据信息。

    结果集元数据ResultSetMetaData： resultSet.getDataMeta获得的比较重要的是表的列名、列的属性等信息。

    结果集元数据对象: ResultSetMetaData meta = rs.getDataMeta();

                  字段个数：meta.getColumnCount();

                  字段名字：meta.getColumnName();

                  字段JDBC类型：meta.getColumnType();

                  字段数据库类型：meta.getColumnTypeName();

    数据库元数据对象： DatabaseMetaData meta = con.getMetaData();

                   数据库名：meta.getDatabaseProductName();

                   数据库版本号：meta.getDatabaseProductVersion();

                   数据库驱动名：meta.getDriverName();

                   数据库驱动版本号：meta.getDriverVersion();

                   数据库URL：meta.getURL();

                   该连接的数据库登录名：meta.getUserName();

来源：https://blog.csdn.net/logo_oo/article/details/80014013



什么是编译型语言和解释型语言？
       计算机是不能理解高级语言的，更不能直接执行高级语言，它只能直接理解机器语言，所以使用任何高级语言编写的程序若想被计算机运行，都必须将其转换成计算机语言，也就是机器码。


       计算机是不能理解高级语言的，更不能直接执行高级语言，它只能直接理解机器语言，所以使用任何高级语言编写的程序若想被计算机运行，都必须将其转换成计算机语言，也就是机器码。而这种转换的方式有两种：

1.编译

2.解释

由此高级语言也分为编译型语言和解释型语言。

主要区别在于，前者源程序编译后即可在该平台运行，后者是在运行期间才编译。所以前者运行速度快，后者跨平台性好。

编译型语言
       使用专门的编译器，针对特定的平台，将高级语言源代码一次性的编译成可被该平台硬件执行的机器码，并包装成该平台所能识别的可执行性程序的格式。

特点
       在编译型语言写的程序执行之前，需要一个专门的编译过程，把源代码编译成机器语言的文件，如exe格式的文件，以后要再运行时，直接使用编译结果即可，如直接运行exe文件。因为只需编译一次，以后运行时不需要编译，所以编译型语言执行效率高。

总结
1.一次性的编译成平台相关的机器语言文件，运行时脱离开发环境，运行效率高；

2.与特定平台相关，一般无法移植到其他平台；

3.现有的C、C++、Objective等都属于编译型语言。




解释型语言
使用专门的解释器对源程序逐行解释成特定平台的机器码并立即执行。是代码在执行时才被解释器一行行动态翻译和执行，而不是在执行之前就完成翻译。

特点
解释型语言不需要事先编译，其直接将源代码解释成机器码并立即执行，所以只要某一平台提供了相应的解释器即可运行该程序。

总结
1.解释型语言每次运行都需要将源代码解释称机器码并执行，效率较低；

2.只要平台提供相应的解释器，就可以运行源代码，所以可以方便源程序移植；

3.Python等属于解释型语言。

编译型与解释型，两者各有利弊
前者由于程序执行速度快，同等条件下对系统要求较低，因此像开发操作系统、大型应用程序、数据库系统等时都采用它，像C/C++、Pascal/Object Pascal（Delphi）等都是编译语言，而一些网页脚本、服务器脚本及辅助开发接口这样的对速度要求不高、对不同系统平台间的兼容性有一定要求的程序则通常使用解释性语言，如Java、JavaScript、VBScript、Perl、Python、Ruby、MATLAB 等等。

作者：KID不务正业的程序员
链接：https://www.jianshu.com/p/54e2aeca013b


用PYTHON语言进行数据库编程, 至少有六种方法可供采用. 我在实际项目中采用,不但功能强大,而且方便快捷.以下是我在工作和学习中经验总结.

方法一:使用DAO (Data Access Objects)

这个第一种方法可能会比较过时啦.不过还是非常有用的. 假设你已经安装好了PYTHONWIN,现在开始跟我上路吧……

找到工具栏上ToolsàCOM MakePy utilities,你会看到弹出一个Select Library的对话框, 在列表中选择'Microsoft DAO 3.6 Object Library'(或者是你所有的版本).

现在实现对数据的访问:

#实例化数据库引擎
import win32com.client
engine = win32com.client.Dispatch("DAO.DBEngine.35")
#实例化数据库对象,建立对数据库的连接
db = engine.OpenDatabase(r"c:/temp/mydb.mdb")

现在你有了数据库引擎的连接,也有了数据库对象的实例.现在就可以打开一个recordset了. 假设在数据库中已经有一个表叫做 'customers'. 为了打开这个表,对其中数据进行处理,我们使用下面的语法:

rs = db.OpenRecordset("customers")
#可以采用SQL语言对数据集进行操纵
rs = db.OpenRecordset("select * from customers where state = 'OH'")

你也可以采用DAO的execute方法. 比如这样:

db.Execute("delete * from customers where balancetype = 'overdue' and name = 'bill'")
#注意,删除的数据不能复原了J

EOF 等属性也是可以访问的, 因此你能写这样的语句:

while not rs.EOF:
 print rs.Fields("State").Value
 rs.MoveNext()
我最开始采用这个方法,感觉不错.

方法二:使用Python DB API,Python ODBC modules(you can use ODBC API directly, but maybe it is difficult for most beginner.)

为了在Python里面也能有通用的数据库接口,DB-SIG为我们提供了Python数据库.(欲知详情,访问DB-SIG的网站,http://www.python.org/sigs/db-sig/).   Mark

Hammond的win32扩展PythonWin里面包含了这些API的一个应用-odbc.pyd. 这个数据库API仅仅开放了一些有限的ODBC函数的功能(那不是它的目的),但是它使用起来很简单,而且在win32里面是免费的.

安装odbc.pyd的步骤如下:

1. 安装python软件包:

http://www.python.org/download/

2. 安装Mark Hammond的最新版本的python win32扩展 - PythonWin:

http://starship.python.net/crew/mhammond/

3. 安装必要的ODBC驱动程序,用ODBC管理器为你的数据库配置数据源等参数

你的应用程序将需要事先导入两个模块:

   dbi.dll   - 支持各种各样的SQL数据类型,例如:日期-dates
   odbc.pyd – 编译产生的ODBC接口

下面有一个例子:

import dbi, odbc   # 导入ODBC模块
import time      # 标准时间模块
dbc = odbc.odbc(   # 打开一个数据库连接
    'sample/monty/spam'  # '数据源/用户名/密码'
    )
crsr = dbc.cursor()  # 产生一个cursor
crsr.execute(     # 执行SQL语言
    """
    SELECT country_id, name, insert_change_date
    FROM country
    ORDER BY name
    """
)
print 'Column descriptions:'  # 显示行描述
for col in crsr.description:
 print ' ', col
result = crsr.fetchall()    # 一次取出所有的结果
print '/nFirst result row:/n ', result[0]  # 显示结果的第一行
print '/nDate conversions:'  # 看看dbiDate对象如何?
date = result[0][-1]
fmt = '  %-25s%-20s'
print fmt % ('standard string:', str(date))
print fmt % ('seconds since epoch:', float(date))
timeTuple = time.localtime(date)
print fmt % ('time tuple:', timeTuple)
print fmt % ('user defined:', time.strftime('%d %B %Y', timeTuple))
下面是结果:

输出(output)

Column descriptions:
  ('country_id', 'NUMBER', 12, 10, 10, 0, 0)
  ('name', 'STRING', 45, 45, 0, 0, 0)
  ('insert_change_date', 'DATE', 19, 19, 0, 0, 1)
First result row:
  (24L, 'ARGENTINA', <DbiDate object at 7f1c80>)
Date conversions:
  standard string:   Fri Dec 19 01:51:53 1997
  seconds since epoch:  882517913.0
  time tuple:    (1997, 12, 19, 1, 51, 53, 4, 353, 0)
  user defined:    19 December 1997
大家也可以去http://www.python.org/windows/win32/odbc.html看看,那儿有两个Hirendra Hindocha写的例子,还不错.

注意, 这个例子中,结果值被转化为Python对象了.时间被转化为一个dbiDate对象.这里会有一点限制,因为dbiDate只能表示UNIX时间(1 Jan 1970 00:00:00 GMT)之后的时间.如果你想获得一个更早的时间,可能会出现乱码甚至引起系统崩溃.*_*

方法三: 使用 calldll模块

(Using this module, you can use ODBC API directly. But now the python version is 2.1, and I don't know if other version is compatible with it. 老巫:-)

Sam Rushing的calldll模块可以让Python调用任何动态连接库里面的任何函数,厉害吧?哈.其实,你能够通过直接调用odbc32.dll里面的函数操作ODBC.Sam提供了一个包装模块odbc.py,就是来做这个事情的.也有代码来管理数据源,安装ODBC,实现和维护数据库引擎 (Microsoft Access).在那些演示和例子代码中,还有一些让人侧目的好东东,比如cbdemo.py,有一个信息循环和窗口过程的Python函数!

[你可以到Sam's Python Software去找到calldll的相关连接,那儿还有其他好多有趣的东西]

下面是安装CALLDLL包的步骤:

1. 安装PYTHON软件包(到现在为止最多支持2.1版本)

2. 下载calldll-2001-05-20.zip:

ftp://squirl.nightmare.com/pub/python/python-ext/calldll-2001-05-20.zip

3. 在LIB路径下面创建一个新路径比如说:

c:/Program Files/Python/lib/caldll/

4. 在原目录下解压calldll.zip

5. 移动calldll/lib/中所有的文件到上面一个父目录(calldll)里面,删除子目录(lib)

6. 在CALL目录里面生成一个file __init__.py文件,象这样:

# File to allow this directory to be treated as a python 1.5
package.

7. 编辑calldll/odbc.py:

在"get_info_word"和"get_info_long"里面,改变"calldll.membuf"为"windll.membuf"

下面是一个怎么使用calldll的例子:

from calldll import odbc
dbc = odbc.environment().connection() # create connection
dbc.connect('sample', 'monty', 'spam') # connect to db
# alternatively, use full connect string:
# dbc.driver_connect('DSN=sample;UID=monty;PWD=spam')
print 'DBMS: %s %s/n' % ( # show DB information
  dbc.get_info(odbc.SQL_DBMS_NAME),
  dbc.get_info(odbc.SQL_DBMS_VER)
  )
result = dbc.query( # execute query & return results
  """
  SELECT country_id, name, insert_change_date
  FROM country
  ORDER BY name
  """
  )
print 'Column descriptions:' # show column descriptions
for col in result[0]:
  print ' ', col
print '/nFirst result row:/n ', result[1] # show first result row

output(输出)

DBMS: Oracle 07.30.0000
Column descriptions:
  ('COUNTRY_ID', 3, 10, 0, 0)
  ('NAME', 12, 45, 0, 0)
  ('INSERT_CHANGE_DATE', 11, 19, 0, 1)
First result row:
  ['24', 'ARGENTINA', '1997-12-19 01:51:53']

方法四: 使用ActiveX Data Object(ADO)

现在给出一个通过Microsoft's ActiveX Data Objects (ADO)来连接MS Access 2000数据库的实例.使用ADO有以下几个好处: 首先,与DAO相比,它能更快地连接数据库;其次,对于其他各种数据库(SQL Server, Oracle, MySQL, etc.)来说,ADO都是非常有效而方便的;再有,它能用于XML和文本文件和几乎其他所有数据,因此微软也将支持它比DAO久一些.

第一件事是运行makepy.尽管这不是必须的,但是它对于提高速度有帮助的.而且在PYTHONWIN里面运行它非常简单: 找到工具栏上ToolsàCOM MakePy utilities,你会看到弹出一个Select Library的对话框, 在列表中选择'Microsoft ActiveX Data Objects 2.5 Library ‘(或者是你所有的版本).

然后你需要一个数据源名Data Source Name [DSN] 和一个连接对象. [我比较喜欢使用DSN-Less 连接字符串 (与系统数据源名相比,它更能提高性能且优化代码)]
就MS Access来说,你只需要复制下面的DSN即可.对于其他数据库,或者象密码设置这些高级的功能来说,你需要去 [Control Panel控制面板 | 管理工具Administrative Tools | 数据源Data Sources (ODBC)]. 在那里,你可以设置一个系统数据源DSN. 你能够用它作为一个系统数据源名,或者复制它到一个字符串里面,来产生一个DSN-Less 的连接字符串. 你可以在网上搜索DSN-Less 连接字符串的相关资料. 好了,这里有一些不同数据库的DSN-Less连接字符串的例子:SQL Server, Access, FoxPro, Oracle , Oracle, Access, SQL Server, 最后是 MySQL.

>>> import win32com.client
>>> conn = win32com.client.Dispatch(r'ADODB.Connection')
>>> DSN = 'PROVIDER=Microsoft.Jet.OLEDB.4.0;DATA SOURCE=C:/MyDB.mdb;'
>>> conn.Open(DSN)

经过上面的设置之后,就可以直接连接数据库了:

首要的任务是打开一个数据集/数据表

>>> rs = win32com.client.Dispatch(r'ADODB.Recordset')
>>> rs_name = 'MyRecordset'
>>> rs.Open('[' + rs_name + ']', conn, 1, 3)

[1和3是常数.代表adOpenKeyset 和adLockOptimistic.我用它作为默认值,如果你的情况不同的话,或许你应该改变一下.进一步的话题请参考ADO相关材料.]

打开数据表后,你可以检查域名和字段名等等

>>> flds_dict = {}
>>> for x in range(rs.Fields.Count):
...  flds_dict[x] = rs.Fields.Item(x).Name

字段类型和长度被这样返回A :

>>> print rs.Fields.Item(1).Type
202 # 202 is a text field
>>> print rs.Fields.Item(1).DefinedSize
50 # 50 Characters

现在开始对数据集进行操作.可以使用SQL语句INSERT INTO或者AddNew() 和Update()

>>> rs.AddNew()
>>> rs.Fields.Item(1).Value = 'data'
>>> rs.Update()

这些值也能够被返回:

>>> x = rs.Fields.Item(1).Value
>>> print x
'data'

因此如果你想增加一条新的记录,不必查看数据库就知道什么number 和AutoNumber 字段已经产生了

>>> rs.AddNew()
>>> x = rs.Fields.Item('Auto_Number_Field_Name').Value 
# x contains the AutoNumber
>>> rs.Fields.Item('Field_Name').Value = 'data'
>>> rs.Update()

使用ADO,你也能得到数据库里面所有表名的列表:

>>> oCat = win32com.client.Dispatch(r'ADOX.Catalog')
>>> oCat.ActiveConnection = conn
>>> oTab = oCat.Tables
>>> for x in oTab:
...  if x.Type == 'TABLE':
...   print x.Name

关闭连接. 注意这里C是大写,然而关闭文件连接是小写的c.

>>> conn.Close()

前面提到,可以使用SQL语句来插入或者更新数据,这时我们直接使用一个连接对象.

>>> conn = win32com.client.Dispatch(r'ADODB.Connection')
>>> DSN = 'PROVIDER=Microsoft.Jet.OLEDB.4.0;DATA SOURCE=C:/MyDB.mdb;'
>>> sql_statement = "INSERT INTO [Table_Name]
([Field_1], [Field_2]) VALUES ('data1', 'data2')"
>>> conn.Open(DSN)
>>> conn.Execute(sql_statement)
>>> conn.Close()

最后一个例子经常被看作是ADO的难点.一般说来,想要知道一个表的RecordCount 的话,必须象这样一个一个地计算他们 :

>>> # See example 3 above for the set-up to this
>>> rs.MoveFirst()
>>> count = 0
>>> while 1:
...  if rs.EOF:
...   break
...  else:
...   count = count + 1
...   rs.MoveNext()

如果你也象上面那样些程序的话,非常底效不说,如果数据集是空的话,移动第一个记录的操作会产生一个错误.ADO提供了一个方法来纠正它.在打开数据集之前,设置CursorLocation 为3. 打开数据集之后,就可以知道recordcount了.

>>> rs.Cursorlocation = 3 # don't use parenthesis here
>>> rs.Open('SELECT * FROM [Table_Name]', conn) # be sure conn is open
>>> rs.RecordCount # no parenthesis here either
186

[再:3是常数]

这些只用到ADO的皮毛功夫,但对于从PYTHON来连接数据库,它还是应该有帮助的.

想更进一步学习的话,建议深入对象模型.下面是一些连接:
http://msdn.microsoft.com/library/default.asp?url=/library/en-us/ado270/htm/mdmscadoobjmod.asp
http://www.activeserverpages.ru/ADO/dadidx01_1.htm

(单步执行还可以，为何写为script就不行？老巫疑惑)

方法五:使用 mxODBC模块(在Windows和Unix下面都可以用,但是是商业化软件,要掏钱的.)下面是相关连接:

http://thor.prohosting.com/~pboddie/Python/mxODBC.html

http://www.egenix.com/files/python/mxODBC.html

来源：https://blog.csdn.net/liuyukuan/article/details/52877602