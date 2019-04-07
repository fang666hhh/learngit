1.  mySQL中的命名也要注意不要命关键字，如order
2.  获得表中最大的id值
```
	Connetion con = DbUtil.getCon();//Dbutil.getCon 是自己写的获得连接及Connetion
			String sql = "select * from movie where id = (select max(id) from movie)";
			stmt = con.prepareStatement(sql);
			ResultSet rs = stmt.executeQuery();
			if(rs.next())
			int count = rs.getInt("id");
			
```
3.很多时候我们都要判断ResultSet是否存在记录, 但是java里ResultSet 这个对象没有提供一个方法能判断 ,我们只能用next这个方法, next会滚动一条记录丢失第一条数据, 往往很多时候都需要第一条记录,所以我们要做相应的处理
>>https://blog.csdn.net/djun100/article/details/9281717
4. 外键设置失败的原因补充：
    原因：
设置的外键和对应的另一个表的主键值不匹配。
解决方法：  
找出不匹配的值修改。
或者清空两表数据。
5. 学会看异常信息，耐心找异常位置（自己写的部分），不懂得单词可以看词典
6. 不懂作标记，超时未解决跳过
7. 将sql查询到的信息封装到实体类再返回，以后用的时更加方便
8. 
```
一、&与&&的异同点。

相同点：二者都表示与操作，当且仅当运算符两边的操作数都为true时，其结果才为true，否则为false。

不同点：在使用&进行运算时，不论左边为true或者false，右边的表达式都会进行运算。如果使用&&进行运算时，当左边为false时，右边的表达式不会进行运算，因此&&被称作短路与。

二、|与||的异同点。

相同点：二者都表示或操作，当运算符两边的操作数任何一边的值为true时，其结果为true，当两边的值都为false时，其结果才为false。

不同点：同与操作类似，||表示短路或，当运算符左边的值为true时，右边的表达式不会进行运算。
```
9. java.util.regex 包主要包括以下三个类：
Pattern 类：
pattern 对象是一个正则表达式的编译表示。Pattern 类没有公共构造方法。要创建一个 Pattern 对象，你必须首先调用其公共静态编译方法，它返回一个 Pattern 对象。该方法接受一个正则表达式作为它的第一个参数。
Matcher 类：
Matcher 对象是对输入字符串进行解释和匹配操作的引擎。与Pattern 类一样，Matcher 也没有公共构造方法。你需要调用 Pattern 对象的 matcher 方法来获得一个 Matcher 对象。
PatternSyntaxException：
PatternSyntaxException 是一个非强制异常类，它表示一个正则表达式模式中的语法错误。
10. 判断两字符串是否同，最后copy后用equals,防止手动打错
11. 如果Vector 的i下标还未赋值，不能用set（i,...）;
12. 错误操作：因为用的都是同一个Order，add的只是一个地址，这样操作最后会得到许全部都一样的order元素

```
//错误
 	ResultSet rs = stmt.executeQuery();
				Vector<Order>orders = new Vector<>();
				 
				//ResultSetMetaData rsmd = (ResultSetMetaData) rs.getMetaData();
				while(rs.next())
				{   
					Order order   =  new Order ();
					order.setId(Integer.valueOf(rs.getString("id")));
					order.setMovie_name(rs.getString("movie_name"));
					order.setOrdertime(rs.getString("ordertime"));
					order.setUser_name(rs.getString("user_name"));
					orders.add(order);
				}
				return new Msg("查询订单成功",orders) ;
			}


//更改
while(rs.next())
				{   
					Order order   =  new Order ();
					order.setId(Integer.valueOf(rs.getString("id")));
					order.setMovie_name(rs.getString("movie_name"));
					order.setOrdertime(rs.getString("ordertime"));
					order.setUser_name(rs.getString("user_name"));
					orders.add(order);
				}
  ```
  13.先对界面传来的数据进行判断出来再进行封装