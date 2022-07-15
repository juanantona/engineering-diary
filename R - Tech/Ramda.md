Placeholder

```
const a = [
	{ pepe:null, pepa:'hola' },
	{ pepe:1, pepa:'hole' }
]
  
const obj = { pepe:null, pepa:'hola' }

const getPepe = R.prop(R.__, obj)

getPepe('pepe') -> null
```




