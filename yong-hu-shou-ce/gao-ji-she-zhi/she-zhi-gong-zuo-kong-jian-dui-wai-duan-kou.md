# 设置工作空间对外端口

如果您需要外部请求调用工作空间服务，请在代码中使用27777端口，工作空间内的27777端口将被映射到公网可访问的调试连接上。

启动成功后，在实例列表的操作栏中，点击复制调试地址进行测试访问。

下面是一个简单的例子，编写一个名为hello.py的脚本，内容如下：

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
 
if __name__=='__main__':
    app.run(port='27777',host='0.0.0.0')
```

执行：

```bash
pip3 install flask
python3 hello.py
```

将调试地址复制到浏览器：

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



