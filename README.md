# navbar-vue

## Navbar configurations

```
navbar: {
  brand: "my-awesome-site", // note: you can use function to return custom component
  links: [
    {
      to: "/about/",
      value: "About", // <a :href="to">{{ value }}</a>
      icon: () => <my-icon />, // optional: custom icon.
    }
  ],
  useAnchor: true, // false will use router-link
  ulClass: "nav-links", // optional: custom class for unordered list
                        // note: without dot !
  liClass: "", // optional: custom class for list item.
  customLinksComponent: () => <my-custom-links-component /> // note: your component should take the same props in link object.
  openClass: "", // optional: custom class for animation on mobile mode
  mobileMode: false // this is a required prop for mobile
}
```

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Run your tests

```
npm run test
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
