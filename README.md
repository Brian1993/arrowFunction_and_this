# arrowFunction_and_this

# 箭頭函式與this的關係

### 在講arrorw function 裡面我們先聊聊 bind 這個 method 

``` javascript 
let user = {
    name : "Jhon",
    func : function(){
        console.log(this)
    }
}
``` 

我們要使用 user 裡面的 func 函式時，通常會用  

``` javascript 
user.func()
```
我們也會得到結果 this 就是 user 這個 object ， 但如果我們換一個寫法

```javascript 
let user = {
    name : "Jhon",
    func : function(){
        console.log(this)
    }
}
let func02 = user.func ; 
func02();
 ```
我們就會得到結果是 this 是 window 或是 global , 為甚麼呢?
因為原本的 func 還在user 這個 object 當中 ，所以 this 會指向 user , 但是 func02 不同，它已經脫離了user這個object所以會指向最上層的
object 也就是 window 或是 global (在node裡)

要處理這個問題的方法就是用 bind 這個 method ，

```javascript
let func02 = user.func.bind(user);
func02()
```
這樣子我們就會得到結果是，this 是 user 這個 object 


### 那這跟 Arrow function 有什麼關係呢？

我們換一個寫法

```javascript 
let user = {
    name : "Jhon",
    func : function(){
        setTimeout(function(){
          console.log(this)
          }, 1000);     
    }
}
user.func()
``` 

我們又會遇到與剛剛相同的問題，this 又指向了 window ， 原因也相同，setTimeout 裡面的 callback function 並不屬於任何 object， 要解決這個問題 ， arrow function 就登場了

```javascript 
let user = {
    name : "Jhon",
    func : function(){
        setTimeout(() = > console.log(this) , 1000);     
    }
}
user.func()
``` 
我們就會得到結果 this 是 user ， 為什麼呢？ 因為 arrow function 會直接繼承 this ， 不會進行 rebind（重新綁定）的動作 





