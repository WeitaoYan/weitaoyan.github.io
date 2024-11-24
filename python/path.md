# 路径拼接

今天遇到一个路径拼接的问题有点意思，记录一下。  
Python中常使用路径拼接函数为`os.path.join`，发现下面三种使用情况结果不太一样，需要注意。  
1. 两个参数包含相同前缀，且是绝对路径  
    ```python
    import os
    root = r"D:\china\shaanxi"
    city = r"D:\china\shaanxi\baoji"
    print(os.path.join(root, city))
    ```
    output:
    ```
    D:\china\shaanxi\baoji
    ```

2. 两个参数包含相同前缀，且是相对路径，这种情况需要注意，最好子目录不包含父目录，否则会拼接成重复前缀。
    ```python
    import os
    root = r"china\shaanxi"
    city = r"china\shannxi\baoji"
    print(os.path.join(root, city))
    ```
    output:
    ```
    china\shaanxi\china\shannxi\baoji
    ```

3. 经过上面两个情况，又想到了另一个异常情况，子目录和父目录不一致。
    ```python
    import os
    root = r"D:\china\shaanxi"
    city = r"D:\china\sichuan\dazhou"
    print(os.path.join(root, city))
    ```
    output:
    ```
    D:\china\sichuan\dazhou
    ```
    结果是，这种情况不会报异常，子目录会替换掉父目录不同的部分。这种情况多半会异常，需要避免。