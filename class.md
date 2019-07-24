# es5去实现es6的继承

```
class Hello {
  constructor(name) {
    this.name = name;
  }

  hello() {
    return 'Hello ' + this.name + '!';
  }

  static sayHelloAll() {
    return 'Hello everyone!';
  }
}

class HelloWorld extends Hello {
  constructor() {
    super('World');
  }

  echo() {
    alert(super.hello());
  }
}

var hw = new HelloWorld();
hw.echo();

alert(Hello.sayHelloAll());
```

```
function Hello(name) {
  this.name = name;
}

Hello.prototype.hello = function hello() {
  return 'Hello ' + this.name + '!';
};

Hello.sayHelloAll = function () {
  return 'Hello everyone!';
};

function HelloWorld() {
  Hello.call(this, 'World');
}

HelloWorld.prototype = Object.create(Hello.prototype);
HelloWorld.prototype.constructor = HelloWorld;
HelloWorld.sayHelloAll = Hello.sayHelloAll;

HelloWorld.prototype.echo = function echo() {
  alert(Hello.prototype.hello.call(this));
};

var hw = new HelloWorld();
hw.echo();

alert(Hello.sayHelloAll());
```
