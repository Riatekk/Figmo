# Wireframer

> A wireframing / ui tool for mocking web-based applications.


## Description

Wireframer is self-hosted Javascript application written in [Vue.js](https://vuejs.org/). All data generated by the application is stored in the browser's localstorage. This project was inspired by [Mockup Designer](https://github.com/fatiherikli/mockup-designer).

![alt text](https://github.com/devimust/wireframer/raw/master/screenshots/screenshot1.png "Screenshot 1")


## Dependencies

- [Vue.js (v2)](https://vuejs.org/)
- [Vuex](https://vuex.vuejs.org/en/intro.html)
- [Bootstrap 4](https://getbootstrap.com/)
- [Material Design icons by Google](https://github.com/google/material-design-icons/)
- [html2canvas](https://github.com/niklasvh/html2canvas)


## Installation

Copy `index.html` and the `dist` folder to a webserver.


## Todo

- [ ] Add more widgets: paragraph, table, navigation
- [ ] Deselect widget when clicking outside canvas
- [ ] Serve icons locally
- [ ] Download localstorage json data
- [ ] Ability to sync localstorage to and from a central storage engine (e.g. Firebase) 


## Build Setup

I welcome contributions - please get in touch with me before attempting larger changes.

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).


## License

[MIT](http://opensource.org/licenses/MIT)

Copyright (c) 2017-present, Rudi Olckers
