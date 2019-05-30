# 基于vue的微信授权（hash模式）

## 1. 授权的目的及时机

目的：用code换token。

时机：与接口交互时，被告知无token或token过期


## 2. 请求的公共方法
```js
import axios from 'axios'
import qs from 'qs'
import {
    baseUrl
} from '../config/env'
import {
    isEmpty,
    Storage
} from "@/assets/js/common.js"

class http {
    static async post(url, data) {
        try {
            let path = window.location.href.split('#')[1];
            Storage.set('path', path)
            let sid = Storage.get('sid')

            if (isEmpty(sid) && data.is_sid != 0) {
                // console.log("非授权页面请求，且sid为空");
                window.location.href = '/'
                return {
                    is_success: false
                };
            }

            let res = await axios({
                url: url + '?sid=' + sid,
                method: 'post',
                baseURL: baseUrl,
                transformRequest: [function (data) {
                    /*  `transformRequest` 允许在向服务器发送前，修改请求数据 */
                    data = qs.stringify(data);
                    return data;
                }],
                transformResponse: [function (data) {
                    /* `transformResponse` 在传递给 then/catch 前，允许修改响应数据 */
                    data = JSON.parse(data)
                    data.is_success = data.status == 200;
                    if (data.status == 401) {
                        Storage.remove("sid")
                        window.location.href = '/'
                        // console.log("页面请求返回401,需重新授权");
                        return
                    }
                    return data
                }],
                data: data
            })
            return new Promise((resolve, reject) => {
                if (res.status != 200) {
                    reject({
                        status: res.status,
                        message: res.statusText
                    });
                    return;
                }
                // 服务器返回数据
                resolve(res.data)
            })
        } catch (err) {
            console.log(err)
        }
    }
    static get(url, params) {
        axios({
            url: url,
            method: 'get',
            baseURL: baseUrl,
            params: params
        })
    }
}
```
> ps：我的通配符路由是授权页面。

## 3. 授权的组件页面

```js
export default {
    data() {
        return {
            path: ""
        };
    },
    methods: {
        authInit() {
            //先拿上一个页面的path，再发请求，每次请求会覆盖path
            this.path = Storage.get("path");
            console.log("path:", this.path);

            /* 执行微信授权 */
            //获取当前页面#号前的url再encode
            let url = encodeURIComponent(window.location.href.split("#")[0]);
            // console.log("url", url);
            let code = WxSdk.wxAuth(url);
            // console.log("code=====", code);
            this.getSid(code);
        },
        async getSid(code) {
            if (isEmpty(code)) {
                return;
            }
            if (!isEmpty(Storage.get("sid"))) {
                this.$router.push({
                    path: this.path
                });
            }
            // console.log("===getSid====");
            let res = await getToken({
                code: code,
                is_sid: 0
            });
            // console.log(res);

            if (res.is_success) {
                Storage.set("sid", res.result.sid);
                this.$router.push({
                    path: this.path
                });
            }
        }
    },
    created() {
        this.authInit();
    },
}
```

## 入口index.html
```js
/* 对页面的url重新组装 */
let currentUrl = window.location.href;
let currentSearch = window.location.search;
let hasCode = currentUrl.indexOf("/?code=") != -1;
if (hasCode) {
    window.location.href = "http://vip.18qy.cn" + "/#/auth" + currentSearch;
}
```


