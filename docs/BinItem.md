# CartItem

![Bin Item Photo](./screenshots/CartItem.PNG)

Item stored in a bin. Here you can modify either change amount or remove item from the bin at all.

## Props

| Prop Name | Type   | Default value | Description         |
|-----------|--------|---------------|---------------------|
| img       | string | 'default'     | Path to image       |
| name      | string | 'Hoodie'      | The name of an item |
| price     | number | 999           | The price           |
| option    | string | 'None / None' | The size and color  |
| quantity  | number | 1             | Amount of items     |
| id        | string | 'none'        | Item's id           |

## State

| Prop Name | Type   | Default value | Description        |
|-----------|--------|---------------|--------------------|
| valueQ    | number | 1             | Amount of an items |

## Functions

### removeItem

Removes item from a redux store.

```js
 function removeItem() {
    dispatch({ type: "cart/removeElement", payload: { _id: id } });
  }
```

### changeValue

Changes amount of the item both in the redux store and in the component itself. Also you cannot make amount less than 1 item.

```js
 function changeValue({ target: { value } }) {
    if (value > 0) {
      dispatch({ type: "cart/changeAmount", payload: { _id: id, number: Number(value) } });
      setValueQ(value);
    }
    else {
      dispatch({ type: "cart/changeAmount", payload: { _id: id, number: 1 } });
      setValueQ(1);
    }
  }
```

```jsx
<div className="cart_item">
  <Link to={`/item/${id}`}>
    <div className="cart_item_photo" style={img === 'default' ? { backgroundImage: `url('${imgNotFound}')` } : { backgroundImage: `url('http://${domain}/static/${img}')` }} />
  </Link>
  <div className="cart_item_options">
    <h2>{name.toUpperCase()}</h2>
    <span className="cart_item_option">{option}</span>
    <span className="cart_item_remove" tabIndex="0" onClick={removeItem}>Remove</span>
  </div>
  <div className="cart_item_info">
    <div>
      {windowSize < 1000 && <span>Price</span>}
      <span>${price.toFixed(2)}</span>
    </div>
    <div>
      {windowSize < 1000 && <span>Quantity</span>}
      <input onChange={changeValue} type="number" value={valueQ} />
    </div>
    <div>
      {windowSize < 1000 && <span>Total</span>}
      <span>${(price * valueQ).toFixed(2)}</span>
    </div>
  </div>
</div>
```
