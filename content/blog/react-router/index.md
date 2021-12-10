---
title: "Learning React Router"
date: "2021-12-12T12:30:03.284Z"
description: "Listing the essentials properties of the package React Router DOM"
---

## BrowserRouter

`import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';`

```js
    <Router>
        <Routes>
            <Route path='/' element={<Home/>} />
            <Route path='/about' element={<About/>} />
        </Routes>
    </Router>
```

[See all attributes at ReactRouter.com](https://v5.reactrouter.com/web/guides/quick-start)

## Link

`import { Link } from "react-router-dom"`

```js
<Link to="/about">About</Link>
```

[See more about Link at ReactRouter.com](https://v5.reactrouter.com/web/api/Link)

## UseLocation

`import { useLocation } from 'react-router-dom';`

The following Button component will only be rendered on Homepage:

```js
const location = useLocation()

return (
    {location.pathname === '/' && (
        <Button />
        )
    }
)
```

_Note: `&&` is a shorter way of using a ternary operator, if you want to state only the truthy outcome_

[See more about Hooks at ReactRouter.com](https://v5.reactrouter.com/web/api/Hooks)