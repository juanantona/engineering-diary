https://stackoverflow.com/questions/64245013/difference-between-jest-mock-and-jest-domock/64247239#64247239


Mockear un componente de Chakra:
```js
jest.mock('@chakra-ui/react', () => {
	const chakra = jest.requireActual('@chakra-ui/react');
	return {
		__esModule: true,
		...chakra,
		Button: jest.fn(({ children, onClick }) => (
				<button onClick={onClick}>{children}</button>
		)),
	};
});
```

sasas