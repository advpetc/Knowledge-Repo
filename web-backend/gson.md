# Gson简介

[Gson](https://github.com/google/gson)是由Google开发的高效率读取分析JSON数据的Java第三方library，目前已经开源在Github上。在repo中可以看到详细的效率分析。

在读取数据的时候，Gson可以帮助将数据序列化(serialization)；同时可以生成数据并且导出成`.ser`类型的文件，这种操作叫做反序列化(deserialization)。基本的操作流程是：
1. 首先建立自己数据库的模型(models)，模型一定要符合真实数据的各个元素的关系。
2. 使用线程安全的file io的library来读取／写入数据。
3. 使用`toJson()`或者`fromJson`来序列化或者反序列化。

# 详细步骤

## 建立模型

使用如下json为事例：
```json
{
    "name": "Peter",
    "info": {
        "school": "USC",
        "year": "junior"
    },
    "friends": [
        {
            "name": "owen",
            "sex": "male",
            "age": 20
        },
        {
            "name": "Tracy",
            "sex": "female",
            "age": 19
        }
    ]
}
```
>文件保存格式为`YOUR_FILENAME.JSON`


生成对应的模型:
```java
// in Project.java file
public class Project {
    private String name;
    private Info info;
    private List<Friends> friends;

    // add your setters and getters methods
    // ...
}

// in Info.java file
public class Info {
    private String school;
    private String year;

    // add your setters and getters methods
    // ...
}

// in Friends.java file
public class Friends {
    private String name;
    private String sex;
    private int age;

    // add your setters and getters methods
    // ...
}
```
>这三个class可以在三个不同的文件里，但是使用了同样的package

变量的命名会和json文件的parse工作直接相关，所有都要一一对应才可以，并且大小写敏感。同样注意每个变量的数据类型。

## 读取文件

然后读取文件，这部分从数据序列化开始：

```java
import com.google.gson.Gson;
import com.google.gson.stream.JsonReader;
import com.google.gson.JsonParseException;
import com.google.gson.JsonSyntaxException;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

JsonReader reader = null;
Gson gson = new Gson();
try {
    reader = new JsonReader(new FileReader(input_json_path));
    Project proj = gson.fromJson(reader, Project.class);
} catch (FileNotFoundException e) {
    System.out.println("That file could not be found.");
} catch (JsonSyntaxException je) {
    System.out.println("That file is not a well-formed JSON file.");
} catch (JsonParseException jp) {
    System.out.println(jp.getMessage());
} finally {
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException ioe) {
            System.out.println(ioe.getMessage());
        }
    }
}
```

这里值得注意的是在读取文件的时候可能会出现path中文件不存在或者json文件格式出错的问题，因此要使用*try catch*的方法来应对。同时在规定path的时候有个小的方法：`String input_json_path = System.getProperty("user.dir") + "/";`可以把当前的relative path得到。不要忘记把JsonReader关闭，这里注意finally里面的东西即使在前面的try catch中有return语句也会执行。

## 写入文件

将json写入文件
```java
Gson gson = new Gson();
Staff obj = new Staff();

// 1. Java object to JSON, and save into a file
gson.toJson(obj, new FileWriter(OutputFile));

// 2. Java object to JSON, and assign to a String
String jsonInString = gson.toJson(obj);
```

反序列化更加轻松，只要将有填充内容的java object使用*toJson*就可以导出，同时也可以生成String类型。


## 总结

* Gson没有field validation，所以要想在parse的时候做处理（类似不接受null类型数据）只能在parse之后手动查找。在[Github issue](https://github.com/google/gson/issues/61)中已经有人提出了改进建议，但是还没具体实施。
* 相比于Gson，还有很多其他的parse json文件的library，可以点击[这里](http://blog.takipi.com/the-ultimate-json-library-json-simple-vs-gson-vs-jackson-vs-json/)
* 模型的命名的大小写要注意。
