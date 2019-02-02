# lianjia-scrawler
[![Licenses](https://img.shields.io/badge/license-bsd-orange.svg)](https://opensource.org/licenses/BSD-3-Clause)

Forked from [XuefengHuang's lianjia-scrawler](https://github.com/XuefengHuang/lianjia-scrawler) and adapted for Hangzhou.

__You can visit http://ChrisLinn.github.io/hz-lianjia-scrawler for the charts I generate.__

## 使用说明
+ 下载源码并安装依赖包
```
1. git clone https://github.com/ChrisLinn/hz-lianjia-scrawler.git
2. cd hz-lianjia-scrawler
# If you'd like not to use [virtualenv](https://virtualenv.pypa.io/en/stable/), please skip step 3 and 4.
3. virtualenv lianjia
4. source lianjia/bin/activate
5. pip install -r requirements.txt
6. python scrawl.py
```

+ 设置数据库信息以及爬取城市行政区信息（支持三种数据库格式）
```
DBENGINE = 'mysql' #ENGINE OPTIONS: mysql, sqlite3, postgresql
DBNAME = 'test'
DBUSER = 'root'
DBPASSWORD = ''
DBHOST = '127.0.0.1'
DBPORT = 3306
CITY = 'hz'
REGIONLIST = [u'xihu', u'xiacheng', u'jianggan', u'gongshu', u'shangcheng', u'binjiang', u'yuhang', u'xiaoshan', u'tonglu1', u'chunan1', u'jiande', u'fuyang', u'linan', u'xiasha']
```

+ 运行 `python scrawl.py`! (请注释16行如果已爬取完所想要的小区信息)

+ 可以修改`scrawl.py`来只爬取在售房源信息或者成交房源信息或者租售房源信息

+ 该程序提供两种方式爬取房源信息，一个是根据行政区，另一个是根据小区名。 但是根据行政区的只显示前100页的数据，对于房源比较多的区，最好通过小区名才能爬全。具体内容请看下一部分。


## 相关爬虫函数介绍
```
行政区列表：
regionlist = [u'xihu', u'xiacheng', u'jianggan', u'gongshu', u'shangcheng', u'binjiang']

小区列表，可通过GetCommunityByRegionlist爬虫得到
communitylist = [u'万科星园', u'上地东里']

根据行政区来爬虫小区信息, 返回regionlist里面所有小区信息。
core.GetCommunityByRegionlist(city, regionlist)

根据行政区来爬虫在售房源信息， 返回regionlist里面所有在售房源信息。
由于链家限制，仅支持爬前100页数据，可使用GetHouseByCommunitylist。
core.GetHouseByRegionlist(city, regionlist)

根据小区来爬虫在售房源房源信息，返回communitylist里面所有在售房源信息。
core.GetHouseByCommunitylist(city, communitylist)

根据行政区来爬虫出租房源信息，返回regionlist里面所有出租房源信息。
由于链家限制，仅支持爬前100页数据，可使用GetRentByCommunitylist。
core.GetRentByRegionlist(city, regionlist)

根据小区来爬虫出租房源信息，返回communitylist里面所有出租房源信息。
core.GetRentByCommunitylist(city, communitylist)

根据小区来爬虫成交房源信息，返回communitylist里面所有成交房源信息。
部分数据无法显示因为这些数据仅在链家app显示
core.GetSellByCommunitylist(city, communitylist)

```


## 分析房源信息
+ 详情请参考[`data`](https://github.com/ChrisLinn/hz-lianjia-scrawler/blob/master/data/lianjia.ipynb)目录

# TODO
+ [我爱我家](https://hz.5i5j.com/)
    * 根据`community_id.txt`文件的小区信息爬取各个小区的成交房源信息。
    + 使用方法
    ```
    在scrawl.py中加入
    import woaiwojia
    woaiwojia.GetSellByCommunitylist()
    ```

