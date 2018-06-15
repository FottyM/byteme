# ByteMe

> A Vue.js project

## Build Setup

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## ES6 Questions ==> qna

## Vue

1.  Write a Vue app to display data in table with the following functionalities

    - [ ] Fixed header row (album.id, album.title, photos.title, photos.thumbnail)
    - [x] Specific fields sortable(album.id,albums.title, photos.title)
    - [x] Searchable on albums.title and photos.title
    - [ ] Scrollable (show 25 rows by default)
    - [ ] Custom filters - album.title
    - [x] Thumbnail should appear as an image Data url:

      - https://jsonplaceholder.typicode.com/albums
      - https://jsonplaceholder.typicode.com/photos

2.  Vue Devtools (on Chrome browser) is visible only in development mode. How do you enable it in production?
    Answer: By setting `Vue.config.devtools = true` in `src/main.js`
