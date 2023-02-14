难点：

1.  针对iOS侧滑无法禁止，加入一层hash路由，利用在url后pushHash  (#back)  方法
```JavaScript
const pushHash = (hash: string, fn: () => void): void => {

  const l = history.listen(() => {

    fn();

    l();

  });

  

  history.push({

    pathname: location.pathname,

    query: location.query,

    hash,

  });

};
```


2.  学会使用sessionStorage