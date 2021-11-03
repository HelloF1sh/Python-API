# Python模块
## xlrd
### read
```python
import xlrd

wb = xlrd.open_workbook(src)
sheet = wb.sheet_by_name(sheet_name)
# sheet = wb.sheet_by_index(index)
for i in range(star, sheet.nrows):
    row = sheet.row_values(i)
		
```
## xlwt

```python
import xlwt

res = [{keys:values},{keys:values},{keys:values},...]
wb = xlwt.Workbook(encoding="utf-8")
ws = wb.add_sheet("sheet1")
## title = ["title", "type", "date", "content"]
rows = len(res)
for row in range(0, rows):
    ws.write(row, 0, res[row]["title"])
    ws.write(row, 1, res[row]["type"])
    ws.write(row, 2, res[row]["date"])
    ws.write(row, 3, res[row]["content"])

wb.save("nytime.xlsx")
```



## csv

### read
```python
import csv

	with open(src, 'r', encoding="utf-8")as r:
		csv_reader = csv.reader(r)
		for i in csv_reader:
			print(i)
```
### write
```python
## 如果CSV文件的首个文字是I或者D 会出现问题，改为id就好了
import csv
	with open(target, 'w', newline='', encoding='GBK')as w:
		csv_writer = csv.writer(w, dialect='excel')
		csv_writer.writerow(["title1", "title2", "title3"])
		for _ in somelist
			csv_writer.writerow(["1","2","3"])
```

## json

### write(dumps)

```python
import json
dic = {'key':'value'}
# 将字典直接转字符串
json_str = json.dumps(dic)
with open(src, 'w', encoding="") as f:
	f.write(json_str)
```
### load(load)
```python
new_dict = json.loads(json_str)
#or
with open(src, 'r')as json_file:
	new_dict = json.load(json_file)
#jsonlines
with open("d://test.json", "r", encoding="utf-8")as r:
    for item in jsonlines.Reader(r):
        print(item)
```
## Pandas

### 读Excel

```python
import pandas as pd
df1 = pd.read_excel(r'D:/source.xlsx)
# 通过 index 指定工作表
df3 = pd.read_excel(file_name, sheet_name=0)

# 指定工作表名称
df4 = pd.read_excel(file_name, sheet_name='Sheet1')
```

### 写Excel

```python
import pandas as pd
import os
# 指定了引擎为xlsxwriter
with pd.ExcelWriter(output_file, engine='xlsxwriter') as writer:    
    df1.to_excel(writer, sheet_name='Sheet1', index=False)
    df2.to_excel(writer, sheet_name='Sheet2', index=False)
```





### 遍历df

```python
for index, row in df.iterrows():
    print(row["c1"], row["c2"])
    
# 或者

for row in df.iterrows():
	print(row)
```











# 爬虫

## request

```python
def getContent(detail_url, regex):
    response = requests.get(detail_url, headers=headers, timeout=5)
    response.encoding = 'utf-8'
    html = response.text
    dom = etree.HTML(html)
    contents = [_.strip().strip("\t").strip("\n") for _ in dom.xpath(regex)]
    return "".join(contents)
    
def saveListPageURLJson():
    regex = '//div[@class="dialog-list"]/div[@class="dialog"]/a/@href'
    page_num = 57
    base_url = "https://www.kepuchina.cn/wiki/yzts/02/index_{}.shtml"
    target = "../天文数据/天文.json"
    star_page = 1
    getListPageURL(base_url=base_url, regex=regex, page_num=page_num, target=target, star_page=star_page)
```

## selenium

```python
driver = webdriver.Chrome()
driver.get(cur_url)
# 显式等待加载
time.sleep(5)
js = ""
driver.execute_script(js)
page = 0
flag = True
while flag:
    try:
        btn = driver.find_element_by_class_name(
            'css-vsuiox').find_element_by_tag_name('button')
        btn.click()
        time.sleep(1)
        page += 1
        print('Fetching data on page {}！！！'.format(page))
        if page % 10 == 0:
            print('The page is loaded and data is being obtained！！！')
            html = driver.page_source
            url_regex = '//div[@class="css-1i8vfl5"]//a/@href'
            section_regex = '//p[@class="css-myxawk"]//text()'
            dom = etree.HTML(html)
            hrefs = dom.xpath(url_regex)
            sections = dom.xpath(section_regex)
            for url, section in zip(hrefs,sections):
                item_id += 1
                temp = dict()
                news_url = "https://www.nytimes.com/" + url
                temp["url"] = news_url
                temp["section"] = section
                temp["id"] = item_id
                res.append(temp)
                if page >= 50:
                    flag = False
                    continue
                    except Exception as e:
                        print(repr(e))
                        flag = False
                        else:
```









## 列表操作

## 除去列表中的空字符串
```python
list1 = ['','',"a"]
lis = list(filter(None,list1))
# lis = ["a"]
# 去除html中的&nbsp
text.replace(u'\xa0', '')
```



# Python基本操作

## 字典操作

### 按照value排序

```python
d={'a':1,'c':3,'b':2}    # 首先建一个字典d
#d.items()返回的是： dict_items([('a', 1), ('c', 3), ('b', 2)])
d_order=sorted(d.items(),key=lambda x:x[1],reverse=False)  # 按字典集合中，每一个元组的第二个元素排列。
                                                           # x相当于字典集合中遍历出来的一个元组。
print(d_order)     # 得到:  [('a', 1), ('b', 2), ('c', 3)]
 
 
    
```



### 找最大Values和其对应的Key

```
>>> a = {"a":1,"b":2,"c":3}
>>> max(a.items(), key=lambda x:x[1])
（'c',3）
```







## 文件操作

#### 复制文件

```python
>>> import shutil
>>> shutil.copyfile('C:\\1.txt', 'D:\\1.txt')

```



#### 创建文件夹

```python
def mkdir(path):
    # 引入模块
    import os
    # 去除首位空格
    path=path.strip()
    # 判断路径是否存在
    # 存在     True
    # 不存在   False
    isExists=os.path.exists(path)
    # 判断结果
    if not isExists:
        # 如果不存在则创建目录
        　# 创建目录操作函数
        os.makedirs(path)
        print path+' 创建成功'
        return True
    else:
        # 如果目录存在则不创建，并提示目录已存在
        print path+' 目录已存在'
        return False
    
# 定义要创建的目录
mkpath="d:\\qttc\\web\\"
# 调用函数
mkdir(mkpath)

```











## Python Linux

```
nohup python -u run.py -model bert> bert.log 2>&1 &
最后的 & 表示在后台运行
2 表示输出错误信息到提示符窗口
1 表示输出信息到提示符窗口，1前面的&要注意添加，否则还会创建一个名为 1 的文件
最后会把日志文件输出到 test.log 文件
```





## Fast API

### gunicorn

```python
# 启动
gunicorn main:app -b 0.0.0.0:2022  -w 4 -k uvicorn.workers.UvicornH11Worker --daemon 
# 查看进程
pstree -ap | grep gunicorn
# 关闭任务
kill -9 主进程端口号
# 重启整个gunicorn任务
kill -HUP 主进程端口号
```


## 命令行操作
### argparse
```python
# 我的理解是 先初始化解析器对象，使用解析器对象生成参数对象，之后再初始化参数对象

# parser是解析器对象
parser = argparse.ArgumentParser()

parser.add_argument('--mode', type=str, default='train', choices=['train', 'test'])
parser.add_argument('--crf', action='store_true')
# ......

# arg 参数对象
args = parser.parse_args()



```





# 数据清洗

### 切分句子

```python
# 切分后不带分隔符的
def cut_sents(text):
    parttern = r'|;|\?|!|。|；|！|？|…'
    res = re.split(parttern, text)
    return [_.replace(" ", "") for _ in res if _]

# 切分后带分隔符的
def cut_sents(text):
    sentences = re.split(r"([.。!！?？；;，,\s+])", text)
    sentences.append("")
    return ["".join(i) for i in zip(sentences[0::2],sentences[1::2])]

```

````
