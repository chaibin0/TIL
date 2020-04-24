# beautify할때 비구조화 정렬할 때

Created: Apr 24, 2020 2:26 PM

원하고자 하는 정렬

```jsx
const { promisify } = require('util')
```

그러나 format document를 하면?

```jsx
const {
	promisify
} = require('util')
```

이렇게 3줄로 변한다.

settings.json에서

```json
"beautify.config": {
    "brace_style": "collapse,preserve-inline"
}
```

을 추가하면 원하고자 하는 정렬을 볼 수 있다.