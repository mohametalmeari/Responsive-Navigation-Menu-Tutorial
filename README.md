**Responsive Navigation Menu Tutorial**

Build a Responsive Navigation Menu with Smooth Transitions in HTML, SCSS, and JavaScript;

First, inside the HTML file, create a burger button:

```html
<div class="menu-btn">
  <span class="menu-btn__burger"></span>
</div>
```

Then, create a navigation menu:

```html
<nav class="nav">
  <ul class="menu-nav">
    <li class="menu-nav__item active">
      <a href="index.html" class="menu-nav__link">
        Home
      </a>
    </li>
    <li class="menu-nav__item">
      <a href="page-1.html" class="menu-nav__link">
        Page One
      </a>
    </li>
    <li class="menu-nav__item">
      <a href="page-2.html" class="menu-nav__link">
        Page Two
      </a>
    </li>
  </ul>
</nav>
```

Inside the SCSS file, create a mixin for smooth transitions:

```scss
@mixin transition-ease {
  transition: all 0.5s ease-in-out;
}
```

Next, add styles for the burger button:

```scss
.menu-btn {
  position: relative;
  z-index: 1;
  height: 20px;
  width: 28px;
  cursor: pointer;
  @include transition-ease;

  &__burger {
    position: absolute;
    right: 0;
    top: 0.5rem;
    width: 28px;
    height: 3px;
    background: black;
    @include transition-ease;

    &::before {
      content: '';
      position: absolute;
      top: -8px;
      width: 28px;
      height: 3px;
      background: black;
      @include transition-ease;
    }

    &::after {
      content: '';
      position: absolute;
      top: 8px;
      width: 20px;
      height: 3px;
      background: black;
      @include transition-ease;
    }

    &.open {
      transform: rotate(360deg);
      background: transparent;

      &::before {
        transform: rotate(45deg) translate(5px, 8px);
      }

      &::after {
        width: 28px;
        transform: rotate(-45deg) translate(3px, -7px);
      }
    }
  }
}
```

And add styles for the navigation menu:

```scss
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  opacity: 0.98;
  visibility: hidden;

  a {
    color: black;
    text-decoration: none;
  }

  &.open {
    visibility: visible;
  }

  .menu-nav {
    padding: 0;
    margin: 0;
    display: flex;
    flex-flow: column wrap;
    align-items: center;
    justify-content: center;
    height: 100vh;
    overflow: hidden;
    background: skyblue;
    list-style: none;
    transform: translateY(-100%);
    @include transition-ease;

    &.open {
      transform: translateY(0);
    }

    &__item {
      transform: translateX(100vw);
      @include transition-ease;

      &.open {
        transform: translateX(0);
      }

      &.active > a {
        color: darkblue;
      }
    }

    &__link {
      display: inline-block;
      font-size: 2rem;
      text-transform: uppercase;
      padding: 2rem 0;
      font-weight: 300;
      @include transition-ease;

      &:hover {
        color: gray;
      }
    }
  }
}
```

Create a delay transition for menu items:

```scss
@for $i from 1 through 4 {
  .menu-nav__item:nth-child(#{$i}) {
    transition-delay: (0.1s * $i) + 0.15s;
  }
}
```

Finally, create media queries to make the menu responsive.

```scss
@media screen and (min-width: 768px) {
  .menu-btn {
    visibility: hidden;
  }

  .nav {
    visibility: visible;

    .menu-nav{
      display: block;
      transform: translateY(0);
      height: 100%;
      background: transparent;
      text-align: right;

      &__item {
        display: inline;
        padding-right: 1.5rem;
      }

      &__link {
        font-size: 1.5rem;
      }
    }
  }
}
```

Now, in the JS file, create a toggle function and add it to an event listener for the burger button:

```js
const menuBtn = document.querySelector('.menu-btn');
const hamburger = document.querySelector('.menu-btn__burger');
const nav = document.querySelector('.nav');
const menuNav = document.querySelector('.menu-nav');
const navItems = document.querySelectorAll('.menu-nav__item');

let showMenu = false;

const toggleMenu = () => {
  if (!showMenu) {
    hamburger.classList.add('open');
    nav.classList.add('open');
    menuNav.classList.add('open');
    navItems.forEach(item => item.classList.add('open'));
    showMenu = true;
  } else{
    hamburger.classList.remove('open');
    nav.classList.remove('open');
    menuNav.classList.remove('open');
    navItems.forEach(item => item.classList.remove('open'));
    showMenu = false;
  }
}

menuBtn.addEventListener('click', toggleMenu);
```

Congrats! You just created your [responsive navigation menu](https://mo-dev.site/Responsive-Navigation-Menu-Tutorial/dist/).
