# MERN Ecommece Practice project 

> ### mern stack এর  প্রাকটিস এর জন্য  ecommerce  প্রজেক্ট করা 

> #### তাই  এই প্রজেক্ট এর ধারাবাহিক কাজ গুলো নোট  আকারে  লিখে রাখলাম 

> ###  STEP - 1
>> আমাদের কে রিএক্ট রাউটার  ইনস্টল করে  app.js   ফাইল এ   রিএক্ট রাউটার এ কানেক্ট করতে হবে



<details>
<summary>React  Router  connect  in App.js </summary>

```javascript
import Product from "./pages/Product";
import Home from "./pages/Home";
import ProductList from "./pages/ProductList";
import Register from "./pages/Register";
import Login from "./pages/Login";
import Cart from "./pages/Cart";
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Redirect,
} from "react-router-dom";
import Success from "./pages/Success";
// import { useSelector } from "react-redux";

const user = true;

const App = () => {
  // const user = useSelector((state) => state.user.currentUser);
  return (
    <Router>
      <Switch>
        <Route exact path="/">
          <Home />
        </Route>
        <Route path="/products/:category">
          <ProductList />
        </Route>
        <Route path="/product/:id">
          <Product />
        </Route>
        <Route path="/cart">
          <Cart />
        </Route>
        <Route path="/success">
          <Success />
        </Route>
        <Route path="/login">{user ? <Redirect to="/" /> : <Login />}</Route>
        <Route path="/register">
          {user ? <Redirect to="/" /> : <Register />}
        </Route>
      </Switch>
    </Router>
  );
};

export default App;

```

</details>

<br/>

> ###  STEP - 2
>> আমাদের   প্রোডাক্টস দেখানো  লাগবে।  আর আমাদের প্রোডাক্ট গুলো দেখানোর প্রসেস গুলো নিম্ব লিস্ট  আকারে  দেওয়া হলো - 
আমাদের   প্রোডাক্টস দেখানো  লাগবে।  আর আমাদের প্রোডাক্ট গুলো দেখানোর প্রসেস গুলো নিম্ব লিস্ট  আকারে  দেওয়া হলো - 

- প্রথমে সকল প্রোডাক্টস দেখতে হবে 
- catagory সিলেক্ট করলে সেই অনুযায়ী দেখতে হবে 
- sort  সিলেক্ট করলে  সেই অনুযায়ী দেখানো লাগবে 

![image not found ](./note-img/shop.gif)

<details>
<summary>Get Products  Code ......    </summary>

```javascript
// product list  compoent  code 
  const location = useLocation();
  const cat = location.pathname.split("/")[2];
  const [filters, setFilters] = useState({});
  const [sort, setSort] = useState("newest");

  const handleFilters = (e) => {
    const value = e.target.value;
    setFilters({
      ...filters,
      [e.target.name]: value,
    });
  };

```
```javascript 
<Container>
    <Navbar />
      <Announcement />
      <Title>{cat}</Title>
      <FilterContainer>
        <Filter>
          <FilterText>Filter Products:</FilterText>

          {/* color  select  */}

          <Select name="color" onChange={handleFilters}>
            <Option disabled>Color</Option>
            <Option>white</Option>
            <Option>black</Option>
            <Option>red</Option>
            <Option>blue</Option>
            <Option>yellow</Option>
            <Option>green</Option>
          </Select>

          {/* product size  select  */}
          <Select name="size" onChange={handleFilters}>
            <Option disabled>Size</Option>
            <Option>XS</Option>
            <Option>S</Option>
            <Option>M</Option>
            <Option>L</Option>
            <Option>XL</Option>
          </Select>
        </Filter>
        <Filter>

          {/* product sort system  */}
          <FilterText>Sort Products:</FilterText>
          <Select onChange={(e) => setSort(e.target.value)}>
            <Option value="newest">Newest</Option>
            <Option value="asc">Price (asc)</Option>
            <Option value="desc">Price (desc)</Option>
          </Select>
        </Filter>

      </FilterContainer>

      {/* pass cat, filters  and sort  value  by props */}
      <Products cat={cat} filters={filters} sort={sort} />

      <Newsletter />
    <Footer />
</Container>

```


</details>


