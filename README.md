# byteme

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

# ES6 Questions

1.  Convert to ES6 Syntax

    ```javascript
    const expense = {
      type: 'Business',
      amount: '$50'
    }
    const { type, amount } = expense
    ```

2.  Palindrome

    ```javascript
    const palindrome = str => {
      if (str === Object(str) || typeof str === 'undefined' || str === null) {
        return
      }
      const regX = /[^A-Za-z0-9]/g
      const loweredStr = `${str}`.toLowerCase().replace(regX, '')
      return (
        loweredStr ===
        loweredStr
          .split('')
          .reverse()
          .join('')
      )
    }
    ```

3.  Finder

    ```javascript
    const fruitPresent = fruit => {
      try {
        if (
          fruit === Object(fruit) ||
          typeof fruit === 'undefined' ||
          fruit === null ||
          typeof fruit === 'number'
        ) {
          throw new TypeError(`${typeof fruit} is not a string`)
        }

        return fruits
          .map(f => f.toLowerCase())
          .includes(`${fruit}`.toLowerCase())
      } catch (e) {
        console.error(e)
      }
    }
    ```

4.  Filter

    - Find the total cost of all products with quantity > n using vanilla JS

      ```javascript
      const CostOfProductForQtyGreaterThan = n =>
        productCart
          .filter(product => product.qty > n)
          .reduce((total, prod) => prod.qty * prod.price + total, 0)
      ```

    - Write a function that can take a product name and return the total cost.

      ```javascript
      const CostOfProduct = searchTerm => {
        const item = productCart.find(item => item.productname === searchTerm)
        if (item) return item.price * item.qty
      }
      ```

5.  `this` context

    - fix the code

    ```javascript
    const team = {
      members: ['Superman', 'Batman', 'Wonder Woman'],
      teamName: 'Justice league',
      teamSummary: function() {
        return this.members.map(function(member) {
          return `${member} is on team ${this.teamName}`
        }, this)
      }
    }
    ```
