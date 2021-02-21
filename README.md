### 04-jsx-tricks
- important thing to remember is that children is just a special prop that we could provide.
- we can add additional props and because of the way that object.assign works, if we wanted to override one of the properties in this props object, then we could do so simply by providing it after we spread those props in the props position for this element.
```
const element = <div id="app/root" {...props} className="not-container" />
```

### 07-prop-types  
React supports a feature called prop-types that allows you to validate the types of props that are being passed to your components when they're rendered. 
eg we're going to have SayHello.propTypes:  
```
SayHello.propTypes = {
  firstName(props, propName, componentName) {
    if (typeof props[propName] !== 'string') {
      return new Error("Hey, the ${componentName} needs the prop ${propName} to be a string, but you passed a ${typeof props[propName]}.")
    }
  }
}
``` 
or better  
```
const PropTypes = {
  string(props, propName, componentName) {
    if (typeof props[propName] !== 'string') {
      return new Error("Hey, the ${componentName} needs the prop ${propName} to be a string, but you passed a ${typeof props[propName]}.")
    }
  }
}
SayHello.propTypes = {
  firstName: PropTypes.string,
  lastName: PropTypes.string
}
```

This is so common that the React team created a package on npm that we can use and I'm going to pull it in from unpackage. it actually creates a global variable here for us called prop-types, then just:  
```
SayHello.propTypes = {
  firstName: PropTypes.string,
  lastName: PropTypes.string
}
const element = <SayHello firstName={false} />
```

in production prop-types are not applied.  
If you want to take things a step further, then you can actually get a Babel plugin that will remove the prop-types from your source code for production. That plugin is called `babel-plugin-transform-react-remove-prop-types`. You could install that and use that in your production build, or many tool kits install and use this by default.  
If you want to learn more about the prop-types that are available, you can go to the [prop-types page on npm](https://www.npmjs.com/package/prop-types). There are a lot of different types that you can use for your components to validate that people are using your components properly.