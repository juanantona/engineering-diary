TAGS: #css  
URL: https://dev.to/alexsergey/css-modules-vs-css-in-js-who-wins-3n25  

The CSS Modules approach wins, since the build system doesn't add something extra to implement it, except for the changed class name. Styled-components due to technical implementation, adds dependency as well as code for runtime handling and styling of.

Such code will be slower, due to the fact that the CSS rendered into the file is processed in parallel, and the CSS-in-JS cannot be rendered into a separate CSS file

Styled components is a lot more overhead because all the styled components need to be complied into stylesheets and mounted to the head by javascript which is a blocking language.

---

URL: https://github.com/stitchesjs/stitches/issues/1026

Stitches is a runtime lib, so it's not currently a lib that the React team would recommend. Furthermore, Stitches is not compatible with React 18's streaming feature. If you don't plan to use streaming, then we consider Stitches v1 stable, and it should work fine for your project. If on the other hand, you want to "future-proof" your project, and remain aligned with the general direction of the industry, you might want to consider a static solution instead.

My point above is that the React team (and the broader front-end community too imo) is not in favour of runtime styling solutions. The general direction things are headed is towards styling solutions that don't have any runtime cost. So if you want to make a "future-proof" decision, that is the data point to track.

---
URL: https://pustelto.com/blog/css-vs-css-in-js-perf/

Don’t use runtime CSS-in-JS if you care about the load performance of your site. Simply less JS = Faster Site.

As you can see runtime CSS-in-JS can have a noticeable impact on your webpage. Mainly for low-end devices and regions with a slower internet connection or more expensive data.

---


La forma en la que CSS-in-JS funciona es que 