# 记录一下axios请求和后端对应的处理

0. html中单独引入axios和qs库

```JavaScript  
<script src="https://cdn.bootcdn.net/ajax/libs/axios/0.26.0/axios.min.js"></script>  
<script src="https://cdn.bootcdn.net/ajax/libs/qs/6.10.3/qs.min.js"></script>

<script>
// cdn方式引用qs库要先实例化一下
var qs = QS;

</script>
```

1. axios默认发送application/json参数时

```JavaScript
// js
<script>
function createNote(content){
    axios({
        url: 'http://127.0.0.1:8081/api/createNote2',
        method: 'post',
        data: {
                content: content
            }
        }).then(function (response){
            console.log(response)
        }).catch(function (error){
            console.log(error)
    });
}
<script>
```

```Java
//Java
// 需要用对象接收，或者用Map<String,Object>接收再解析
@PostMapping("/createNote2")
public void CreateNote(@RequestBody Note note){
    noteService.createNote(note.getContent());

}
```

2. 使用qs库处理后发送application/x-www-form-urlencoded格式参数

```Javascript
<script>
function createNote(content){
    const qs = Qs;
        axios({
            url: 'http://127.0.0.1:8081/api/createNote',
            method: 'post',
            data: qs.stringify({content: content})
        }).then(function (response){
            console.log(response)
        }).catch(function (error){
            console.log(error)
        })
}
</script>
```

```Java
// 接收application/x-www-form-urlencoded或multipart/form-data格式的参数
@PostMapping("/createNote")
public void CreateNote(@RequestParam String content){
    noteService.createNote(content);
}
