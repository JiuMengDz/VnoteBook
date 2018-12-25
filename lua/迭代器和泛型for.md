# 1. 迭代器和泛型for
## 1.1. 迭代器
所有的迭代器都需要在连续的调用之间保存一些状态，以便下次调用时知道当前迭代所处的位置及如何从当前位置步进到下一位置

**注意无状态迭代器的调用方式**
她会返回两个参数，控制变量和不可变状态表
并且以此继续调用迭代函数
也就是说如果**控制变量的值**不正确，得到的结果也会不正确
例子：

``` lua
function diQueen.genValueWithoutStatu(table)
     return iter, table, table.first - 1
end

function iter(table, index)
     index = index + 1
     if index < 0 then
          local value = table[index]
          return value    -- 在这里，第二次调用该迭代函数的时候就会以value作为index调用
     else
          if index <= table.last then
               local value = table[index]
               index = index + 1
               return value
          end
     end
     return nil
end
```

修改以上函数的方式也很简单，将正确的index返回即可避免下一次调用时使用了value作为参数调用迭代函数

``` lua
function diQueen.genValueWithoutStatu(table)
     return iter, table, table.first - 1
end

function iter(table, index)
     index = index + 1
     if index < 0 then
          local value = table[index]
          return index , value   
     else
          if index <= table.last then
               local value = table[index]
               index = index + 1
               return index , value
          end
     end
     return nil
end
```