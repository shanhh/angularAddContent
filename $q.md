### $q

angular中的一种promise的一种状态

通过$q.defferd 构建defferd的实例

```javascript
var defferd = $q.deffe();
```

控制台输出defferd

```javascript
notify:function (n) //表明promise对象unfulfilled状态，在resolve或reject之前可以被多次调用。

promise:a
$$state:Object
error:function (fn)
success:function (fn)
__proto__:Object

reject:function (n)//表明promise对象由pending状态转变为rejectedz。
resolve:function (n)//表明promise对象由pending状态转变为resolve。
```

用法 建立一个工厂 专门的存放发送的请求

```javascript
angular.module('MyAPP', []).factory('RequsetService', ['$http', '$q', function($http, $q){
  return {
    getData: function(params){
      var url = 'www/baidu.com',
          deferred = $q.defer();
      $http.post(url, params)
      .success(function(json){
        deferred.resolve(json);
      })
      return defferred.promise;
    }
  }
}])
```

各个页面依赖注入

```javascript
angular.module('MyAPP', []).controller('MyCtrl', ['$scope', 'RequsetService', function($scope, RequsetService){
  let vm = $scope.vm = {};
  /*操作*/
  vm.sendRequest = sendRequest;
  function sendRequest(){
    let params = {
      name: vm.name,
      id: vm.id
    }
    RequsetService.getData(params)
      .success(function(json){
        console.log(json);
      	/*处理数据*/
      })
  }
}])
```