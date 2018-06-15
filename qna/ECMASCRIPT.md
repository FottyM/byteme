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

    - Fix the code

    ```javascript
    const team = {
      members: ['Superman', 'Batman', 'Wonder Woman'],
      teamName: 'Justice league',
      teamSummary: function() {
        return this.members.map(function(member) {
          return `${member} is on team ${this.teamName}`
        }, this) // <---this
      }
    }
    ```

    - Explanations:
      The reason why the code doesn't work(works partially), it is because the callback function in `map` didn't know what `this` was refering too, hence it returned `undefined`, by specifying `this` as the second argument of `map`(see [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)) to tell the function that `this` is making reference to the `object team`
