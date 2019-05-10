# markdown原样显示\# \* &gt;

加\转义

> \\# \\* \&gt;

# 标题

使用1-6个\#

> \#  
> \#\#  
> \#\#\#  
> \#\#\#\#  
> \#\#\#\#\#  
> \#\#\#\#\#\#

# 段落

一个以上的空行则会划分出不同的段落

> Now is the time for all good men to come to  
> the aid of their country. This is just a  
> regular paragraph.
>
> The quick brown fox jumped over the lazy  
> dog's back.

# 区块引用

使用'&gt;'号，多行使用多个'&gt;'

> &gt; This is a blockquote.
>
> &gt; This is the second paragraph in the blockquote.
>
> &gt; \#\# This is an H2 in a blockquote

#### 效果如下

> This is a blockquote.
>
> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote

# 无序列表

> \*   Red  
> \*   Green  
> \*   Blue

#### 效果如下

* Red
* Green
* Blue

# 有序列表

有序列表则使用数字接着一个英文句点

> 1. Red
> 2. Green
> 3. Blue

#### 效果如下

1. Red
2. Green
3. Blue

# 代码

> \`\`\`  
> public HashMap\(int initialCapacity, float loadFactor\) {  
>         if \(initialCapacity &lt; 0\)  
>             throw new IllegalArgumentException\("Illegal initial capacity: " +  
>                                                initialCapacity\);  
>         if \(initialCapacity &gt; MAXIMUM\_CAPACITY\)  
>             initialCapacity = MAXIMUM\_CAPACITY;  
>         if \(loadFactor &lt;= 0 \|\| Float.isNaN\(loadFactor\)\)  
>             throw new IllegalArgumentException\("Illegal load factor: " +  
>                                                loadFactor\);  
>         this.loadFactor = loadFactor;  
>         this.threshold = tableSizeFor\(initialCapacity\);  
>     }  
> \`\`\`

### 效果如下

```
public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
        this.loadFactor = loadFactor;
        this.threshold = tableSizeFor(initialCapacity);
    }
```



