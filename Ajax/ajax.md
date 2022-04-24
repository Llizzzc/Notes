# Ajax
> 1. [黑马教程](https://www.bilibili.com/video/BV1ji4y1876Y?p=11 "ajax")
> 2. [尚硅谷](https://www.bilibili.com/video/BV1WC4y1b78y?p=6 "ajax")

## 一、普通实现
### 1.get请求
+ ```javascript
	// 基本步骤
	<script>
	var xhr = new XMLHttpRequest();	// 创建ajax对象
	xhr.open('get', 'http://localhost:8080/first');	// 指定get请求和地址
	xhr.onreadystatechange = function() {
		console.log(xhr.readyState);
		// 监听ajax状态码，0为创建了还没配置，1为配置了还没发送，2为已经发送，3为已接受到服务器的部分数据，4为已接受完成
	}	// 需要写在send之前
	xhr.send();	// 发送请求
	xhr.onload = function() {
		var responseText = JSON.parse(xhr.responseText);	// 拿到服务器返回的数据
	  xhr.status	// 可以获取http状态码，
		console.log(responseText);
	}
	</script>
	```
+ ```javascript
	// 传递参数
	<body>
    <input type="text" id="name" autocomplete="off"><br />
    <input type="text" id="age"><button>提交</button>
    <script>
        var username = document.querySelector('#name');
        var age = document.querySelector('#age');
        var btn = document.querySelector('button');
        btn.addEventListener('click', function () {
            var xhr = new XMLHttpRequest();
            var nameValue = username.value;
            var ageValue = age.value;
            // 参数需要拼接成Arg1&Arg2这种格式
            // get的请求格式只能是application/x-www-form-urlencoded
            var params = 'username=' + nameValue + '&age=' + ageValue;
            // 地址后带？号再加参数
            xhr.open('get', 'http://localhost:8080/first?' + params);
            xhr.send();
            xhr.onload = function () {
                var responseText = JSON.parse(xhr.responseText);
                console.log(responseText);
            }
        })
    </script>
	</body>
	```
### 2.post请求
+ ```javascript
	<body>
    <input type="text" id="name" autocomplete="off"><br />
    <input type="text" id="age"><button>提交</button>
    <script>
        var username = document.querySelector('#name');
        var age = document.querySelector('#age');
        var btn = document.querySelector('button');
        btn.addEventListener('click', function () {
            var xhr = new XMLHttpRequest();
            var nameValue = username.value;
            var ageValue = age.value;
            var params = 'username=' + nameValue + '&age=' + ageValue;
            xhr.open('post', 'http://localhost:8080/first');
            // post需要设置请求格式
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.send(params);	// 将参数放入send传递
            xhr.onload = function () {
                var responseText = JSON.parse(xhr.responseText);
                console.log(responseText);
            }
        })
    </script>
	</body>
	```
+ ```javascript
	<body>
    <input type="text" id="name" autocomplete="off"><br />
    <input type="text" id="age"><button>提交</button>
    <script>
        var username = document.querySelector('#name');
        var age = document.querySelector('#age');
        var btn = document.querySelector('button');
        btn.addEventListener('click', function () {
            var xhr = new XMLHttpRequest();
            var nameValue = username.value;
            var ageValue = age.value;
            xhr.open('post', 'http://localhost:8080/first');
            // 请求格式为json
            xhr.setRequestHeader('Content-Type', 'application/json');
            params = JSON.stringify({username: nameValue, age: ageValue});	// 将参数转为json传递
            xhr.send(params);
            xhr.onload = function () {
                var responseText = JSON.parse(xhr.responseText);
                console.log(responseText);
            }
        })
    </script>
	</body>
	```

## 二、封装
+ ```javascript
	<script>
        function ajax(options) {
            var defaults = {
                type: 'get',
                url: '',
                data: {},
                header: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                },
                success: function () {}
            };
            Object.assign(defaults, options);	// 使用用户的参数覆盖默认值
            var xhr = new XMLHttpRequest();
            var params = '';
            // 拼接字符串
            for (var attr in defaults.data) {
                params += attr + '=' + defaults.data[attr] + '&';
            }
            params = params.substr(0, params.length - 1);
            if (defaults.type == 'get') {
                defaults.url = defaults.url + '?' + params;
            }
            xhr.open(defaults.type, defaults.url);
            if (defaults.type == 'post') {
                var contentType = defaults.header['Content-Type'];
                xhr.setRequestHeader('Content-Type', contentType);
                if (contentType == 'application/json') {
                    xhr.send(JSON.stringify(defaults.data));
                } else {
                    xhr.send(params);
                }
            } else {
                xhr.send();
            }
            xhr.onload = function () {
                defaults.success(xhr.responseText);
            }
        }
        ajax({
            type: 'post',
            url: 'http://localhost:8080/first',
            data: {
                name: 'dell',
                age: 11
            },
            success: function (data) {
                console.log(data);
            }
        });
    </script>
	```