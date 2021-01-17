中间件 `next` 执行时可能有异步，所以无法保障执行顺序。

```javascript
app.use((ctx, next) => {
    next()
})

app.use((ctx, next) => {
    next()
})
```

**koa中间件 会包装promise作为`next()` 的返回值，**

所以只要把`app.use(fn)`的回调函数强制包裹 `async` `await` 即可保证执行顺序。

```javascript
app.use(async(ctx, next) => {
    // xxx
    await next()
    // xxx
})

app.use(async(ctx, next) => {
    // xxx
    await next()
    // xxx
})
```

