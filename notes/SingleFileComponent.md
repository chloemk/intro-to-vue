# [8] Single File Component

# props 구현 복습

아래의 예제는 상위 컴포넌트에서 AppChild라는 하위 컴포넌트에게 propsdata라는 props를 넘겨주는 예제입니다.

```js
<template>
  <div>
    <AppChild v-bind:propsdata='str'></AppChild>
  </div>
</template>

<script>
import AppChild from './components/AppChild.vue'

export default = {
  data: function() {
    return {
      str: '넘겨주는 데이터 정보',
    };
  },
  components: {
    'app-child': AppChild,
  },
};
</script>
```

하위 컴포넌트는 다음과 같이 propsdata라는 props를 받을 수 있습니다.

```js
<template>
  <div>
    {{propsdata}}
  </div>
</template>

<script>
  export default {
    props: ['propsdata']
  }
</script>
```

---

# event emit 구현 복습

버튼을 클릭하면 `v-on:click='이벤트메서드이름'` sendEvent라는 이벤트가 실행됩니다. 실행됬을 때 `this.$emit('보낼이벤트이름')` 안에 정의한 이벤트가 상위 컴포넌트로 전달됩니다.
상위 컴포넌트에서는 `v-on:받은이벤트이름='상위컴포넌트의메서드이름'` 으로 받을 수 있습니다.
아래의 예제의 같은 경우 상위 컴포넌트의 메서드 이름을 this.str로 변경해주고 있습니다. 여기서의 this는 그 객체 안을 바라보게 됩니다. this.str은 data의 str이 됩니다.

```js
//자식 컴포넌트
<template>
  <button v-on:click='sendEvent'></button>
</template>

<script>
export default {
  methods: {
    sendEvent: function() {
      this.$emit('renew');
    }
  }
}
</script>


//부모 컴포넌트
<template>
  <div>
    <app-child v-on:renew='renewStr'>
      {{str}}
    </app-child>
  </div>
</template>

<script>
import AppChild from './components/AppChild.vue';

export default {
  data: function() {
    return {
      str: '원본str',
    };
  },
  components: {
    'app-child': AppChild,
  },
  methods: {
    renewStr: function () {
      this.str = '다른str',
    };
  },
};
</script>
```
