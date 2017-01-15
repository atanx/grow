```sh
sh
$scrapy startproject tutorial
$scrapy genspider 爬虫名 域名
```
### 2. 定义Item

```
import scrapy

class DmozItem(scrapy.Item):
    title = scrapy.Field()
    link = scrapy.Field()
    desc = scrapy.Field()
```


### 3.编写爬虫
> xpath解析
```python
title = response.xpath(u'//div[@id="title"]/text()').extract_first()
```
> 创建item
```python
item={'title': title, 'link':link, 'desc':desc}
yield item
```

> 创建新请求
```python
yield scrapy.Request(url, self.parse)
```

### 4.爬取

```bash
$scrapy crawl fast -s CLOSESPIDER_ITEMCOUNT=10
$scrapy crawl fast -s CLOSESPIDER_PAGECOUNT=10
$scrapy crawl fast -s CLOSESPIDER_TIMEOUT=10
#爬取参数
$scrapy crawl fast -a category=nt
```

## 使用Pipline
 
## settings
CONCURRENT_REQUESTS = 100
REACTOR_THREADPOOL_MAXSIZE = 20
LOG_LEVEL = 'INFO'
COOKIES_ENABLED = False
RETRY_ENABLED = False
DOWNLOAD_TIMEOUT = 15
REDIRECT_ENABLED = False
AJAXCRAWL_ENABLED = True
