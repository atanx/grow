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
```python
CONCURRENT_REQUESTS = 100  # 并发Requests数
REACTOR_THREADPOOL_MAXSIZE = 20 # Reactor最大线程数
LOG_LEVEL = 'INFO' # 日志级别
COOKIES_ENABLED = False # 禁用Cookie
RETRY_ENABLED = False   # 重试
DOWNLOAD_TIMEOUT = 15   # 超时，s
REDIRECT_ENABLED = False # 重定向
AJAXCRAWL_ENABLED = True # ajax抓取使能
```

## 选择器
### Xpath选择器
```python
# response中提取class包含"adbl-result-item"的li
books = response.xpath('//li[contains(@class, "adbl-result-item")]')
for book in books:
    #提取一个li中的图片src,注意相对路径".//"的使用
    image = book.xpath('.//img[@class="adbl-prod-image"]/@src').extract_first() or ""
    # xpath contains中使用相对路径，选择指定位置的span
    # 下面的语句功能：选择book中特定的li下的第二个span中的文本，
    # 该特定li的第一个span的文本包含"Release Date"
    release_date = book.xpath('.//li[contains(./span/text(),"Release Date")]/span[2]/text()').extract_first() or ''
```

### CSS选择器
