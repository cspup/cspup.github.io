# 异常处理

## 起因
0. 异常没有在控制台输出信息。
1. 发现在过滤器中有一个catch块将Exception捕捉却没处理，导致后面都没有再处理这个异常了，也就没在控制台输出。  
原代码：
   
```Java
        } catch (Exception e) {
            response.setStatus(HttpStatus.UNAUTHORIZED.value());
            ResponseUtil.out(response, R.error(e.getMessage()));
        }
```

## 处理方式  

不应捕捉不处理的异常。