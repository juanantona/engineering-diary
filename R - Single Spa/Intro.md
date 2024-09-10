- In browser modules
- Build-time modules (bundlers)


El paquete `webpack-config-single-spa-react-ts` añade como externals por defecto:
- single-spa
- react
- react-dom

Y esta configuración no puede ser cambiada
https://github.com/single-spa/create-single-spa/blob/e5b4fd4f58d2083b49287c9bcd5a4a30c7fa191c/packages/webpack-config-single-spa-react/lib/webpack-config-single-spa-react.js#L12


Esta la opción de usar este plugin:
https://github.com/single-spa/standalone-single-spa-webpack-plugin

Tener diferentes versiones de React:
https://github.com/single-spa/single-spa/issues/314#issuecomment-620727254

Para hacer posible la importación cruzada de microfrontales, configura tu bundler para que los microfrontales sean tratados como "externos" (webpack docs / rollup docs). Marcarlos como externos garantiza que se traten como módulos dentro del navegador en lugar de módulos en tiempo de compilación.

Video tutoriales:
- [In-browser vs build-time modules](https://www.youtube.com/watch?v=Jxqiu6pdMSU&list=PLLUD8RtHvsAOhtHnyGx57EYXoaNsxGrTU&index=2)
- [Import Maps](https://www.youtube.com/watch?v=Lfm2Ge_RUxs&list=PLLUD8RtHvsAOhtHnyGx57EYXoaNsxGrTU&index=3)
- [Local development with import map overrides](https://www.youtube.com/watch?v=vjjcuIxqIzY&list=PLLUD8RtHvsAOhtHnyGx57EYXoaNsxGrTU&index=4)


