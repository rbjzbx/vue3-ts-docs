# Vueuse学习

# 1.什么是VueUse

如果你了解`react`的`hook`，那么`VueUse`可以看做是`vue`版的`hook`库。如果不太了解，简单概括的话，`VueUse`是基于`Composition API`的常用函数集合。功能类似于`lodash`，免去用户自己去重复写一些常见的函数，如：防抖、节流、fetch等。

# 2.UssFetch

## 2.1useFetch

```vue
<template>
  <div>
    <transition>
      <p v-if="isFetching">
        loading: {{isFetching}}
      </p>
    </transition>
    <template v-if="!isFetching">
      <p>
        接口返回：data => {{data}}
      </p>
      <br />
      <p>
        接口返回：error => {{error}}
      </p>
    </template>
  </div>
</template>

<script setup lang="ts">
import { useFetch } from '@vueuse/core';

const { isFetching, error, data } = useFetch('https://httpbin.org/get');
</script>

```

## 2.2拦截器

```typescript
import { useFetch } from '@vueuse/core';

const { isFetching, error, data } = useFetch('https://httpbin.org/get', {
  beforeFetch({ url, options, cancel }) {
    options.headers = {
      ...options.headers,
      Authorization: `hello world`,
    };

    return {
      options,
    };
  },
  afterFetch(ctx) {
    if (ctx.data.title === 'HxH') ctx.data.title = 'Hunter x Hunter';

    return ctx;
  },
  onFetchError(ctx) {
    if (ctx.data === null) ctx.data = { title: 'Hunter x Hunter' };

    ctx.error = new Error('Custom Error');

    return ctx;
  },
});

```

## 2.3.请求方式与相应格式

```typescript
// get请求参数直接url拼接
const { isFetching, data, error } = useFetch('https://httpbin.org/get?id=1&name=111').get().text();

// post、put、delete在对应方法中传参
const { isFetching, data, error } = useFetch('https://httpbin.org/get')
   .post({ id: 1, name: 111 })
   .json();

// 也可以通过useFetch配置参数进行配置
const { isFetching, data, error } = useFetch(
  'https://httpbin.org/get',
  {
    method: 'POST',
    body: JSON.stringify({
      id: 1,
      name: 111,
    }),
  },
  { refetch: true }
).json()

```


