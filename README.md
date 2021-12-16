镜像


[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/用户名/项目名) 



<details>
<summary>可以使用Cloudflare的Workers来中转流量，（推荐）1配置为：</summary>

```js
const SingleDay = 'xxx.herokuapp.com'
const DoubleDay = 'xxx.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
</details>

<details>
<summary>可以使用Cloudflare的Workers来中转流量，2配置为：</summary>

```js
addEventListener(
  "fetch", event => {
    let url = new URL(event.request.url);
    url.host = "xxx.herokuapp.com";
    let request = new Request(url, event.request);
    event.respondWith(
      fetch(request)
    )
  }
)
```
</details>
