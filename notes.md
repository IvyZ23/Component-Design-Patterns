### Component Design Patterns

#### Props

**Use object syntax to define props:**

`

<script> 
    export default { 
        props: { 
            title: { 
                type: String, 
                required: true 
            }, 
            length: { 
                type: Number, 
                required: true, 
                default: 90 
            }, 
            image: { 
                type: String, 
                default:'../src/randomimage.png' 
            }
    } 
    } 
</script>

`

1. What data type(s) is it? (string, number, boolean, array, object, date, function, symbol)

   - Multiple data types can be provided by defining it with an array

2. Is this prop critical? Does the component need to have ti all time? (add required property of true)

3. Can you provide a default state? (anything by default)
   - By setting a default value, the prop is "required", but there is now a default value to fall back on (pass prop to overwrite it)
