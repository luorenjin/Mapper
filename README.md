#MyBatis通用Mapper3

##极其方便的使用MyBatis单表的增删改查

##支持单表操作，不支持通用的多表联合查询

##优点?

通用Mapper都可以极大的方便开发人员。可以随意的按照自己的需要选择通用方法，还可以很方便的开发自己的通用方法。

为了让您更方便的了解这通用Mapper，这里贴一段代码来看实际效果。

##通用Mapper2

目前最新的Mapper3版本改动很大，如果正在使用2.x版本，可以去看2.x版本的文档：

[Mapper2.x版本首页http://git.oschina.net/free/Mapper2](http://git.oschina.net/free/Mapper2)

如果想同时使用Mapper3和Mapper2中的EntityMapper和SqlMapper，看这里：http://git.oschina.net/free/EntityMapper

##Mapper2.x升级Mapper3注意事项

请看[Mapper2.x升级Mapper3](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/8.UpdateTo3.md)

##通用Mapper3

全部针对单表操作，每个实体类都需要继承通用Mapper接口来获得通用方法。

示例代码：

    CountryMapper mapper = sqlSession.getMapper(CountryMapper.class);
    //查询全部
    List<Country> countryList = mapper.select(new Country());
    //总数
    Assert.assertEquals(183, countryList.size());

    //通用Example查询
    Example example = new Example(Country.class);
    example.createCriteria().andGreaterThan("id", 100);
    countryList = mapper.selectByExample(example);
    Assert.assertEquals(83, countryList.size());

    //MyBatis-Generator生成的Example查询
    CountryExample example2 = new CountryExample();
    example2.createCriteria().andIdGreaterThan(100);
    countryList = mapper.selectByExample(example2);
    Assert.assertEquals(83, countryList.size());

CountryMapper代码如下：

    public interface CountryMapper extends Mapper<Country> {
    }

这里不说更具体的内容，如果您有兴趣，可以查看下面的<b>项目文档</b>

##实体类注解

从上面效果来看也能感觉出这是一种类似hibernate的用法，因此也需要实体和表对应起来，因此使用了JPA注解。更详细的内容可以看下面的<b>项目文档</b>。

Country代码：

    public class Country {
        @Id
        private Integer id;
        @Column
        private String countryname;
        private String countrycode;
        //省略setter和getter方法
    }
    
[使用Mapper专用的MyBatis Generator插件](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper/5.UseMBG.md) 可以方便的生成这些（带注解的）实体类。

##通用Mapper支持Mybatis-3.2.4及以上版本 

##[更新日志](http://git.oschina.net/free/Mapper/blob/master/wiki/Changelog.md)

##Maven坐标以及下载地址

###最新版本3.1.0 - 2015-06-10

* 基础包名从`com.github.abel533`改为`tk.mybatis.mapper`
* Maven的groupId改为`tk.mybatis`,artifactId为`mapper`
* 增加和Example功能类似的Condition查询，仅仅名字不同
* 更多详细变化请看[Mapper3通用接口大全](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/5.Mappers.md)
* 关于3.0.x版本请看[Mapper3.0.x](http://git.oschina.net/free/Mapper/tree/Mapper3.0.x/)

###3.0.0 - 2015-06-04

* 将`EntityMapper`和`SqlMapper`移出，现在是独立项目[EntityMapper](http://git.oschina.net/free/EntityMapper)
* 将`Mapper<T>`全部接口方法拆分为独立接口，方便选择集成
* 增加`MySqlMapper<T>`包含批量插入和单个插入，批量插入可以回写全部id
* 增加`RowBoundsMapper<T>`包含两个分页查询，可以配合[PageHelper](http://git.oschina.net/free/Mybatis_PageHelper)实现物理分页
* 详细变化请看[Mapper3变化](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/1.Changes.md)
* Mapper2资深用户请看[Mapper3高级应用](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/4.Professional.md)
* [Mapper3通用接口大全](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/5.Mappers.md)
* [快速开发自己的通用接口](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/6.MyMapper.md)

##使用Maven

###重要提示,3.1.0及以后版本的groupId修改为tk.mybatis，artifactId为mapper

```xml
<dependency>
    <groupId>tk.mybatis</groupId>
    <artifactId>mapper</artifactId>
    <version>3.1.0</version>
</dependency>
```

##引入Jar包，下载地址：

https://oss.sonatype.org/content/repositories/releases/tk/mybatis/mapper

http://repo1.maven.org/maven2/tk/mybatis/mapper

由于通用Mapper依赖JPA，所以还需要下载persistence-api-1.0.jar：

http://repo1.maven.org/maven2/javax/persistence/persistence-api/1.0/

##项目文档

###通用Mapper 3

1. [Mapper3变化](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/1.Changes.md)

2. [如何集成通用Mapper](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/2.Integration.md)

3. [如何使用通用Mapper](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/3.Use.md)

4. [高级应用](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/4.Professional.md)

5. [Mapper3通用接口大全](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/5.Mappers.md)

6. [快速开发自己的通用接口](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/6.MyMapper.md)

7. [如何使用Mapper专用的MyBatis Generator插件](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/7.UseMBG.md)

8. [在Spring4中使用通用Mapper](http://git.oschina.net/free/Mapper2/blob/master/wiki/mapper/4.Spring4.md)

9. [Mapper3常见问题和用法](http://git.oschina.net/free/Mapper/blob/master/wiki/mapper3/9.QA.md)

###通用Mapper 2

[Mapper2.x首页](http://git.oschina.net/free/Mapper2)

##作者信息

作者博客：http://blog.csdn.net/isea533

作者邮箱： abel533@gmail.com

Mybatis工具群： 211286137 (Mybatis相关工具插件等等)

推荐使用Mybatis分页插件:[PageHelper分页插件](https://github.com/pagehelper/Mybatis-PageHelper)