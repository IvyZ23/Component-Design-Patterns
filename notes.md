### Component Design Patterns

#### Props

---

**Use object syntax to define props:**

```
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
```

1. What data type(s) is it? (string, number, boolean, array, object, date, function, symbol)

   - Multiple data types can be provided by defining it with an array

2. Is this prop critical? Does the component need to have ti all time? (add required property of true)

3. Can you provide a default state? (anything by default)
   - By setting a default value, the prop is "required", but there is now a default value to fall back on (pass prop to overwrite it)

**Prop Validator**

```
validator: propValue => {
    const propExists = propValue.length > 0

    return propExists
}
```

The above validator checks if the length of the string is longer than zero.

```
<script>
    export default {
        props: {
            image: {
                type: String,
                default: '/src/randomimg.png',
                validator: propValue => {
                    const hasImagesDirectory = propValue.indexOf('/src/') > -1
                    const isPNG = propValue.endWith('.png')
                    const isJPEG = propValue.endWith('.jpeg') || propValue.endWith('.jpg')
                    const hasValidExtension = isPNG || isJPEG

                    return hasImagesDirectory && hasValidEntension
                }
            }
        }
    }
</script>
```

The above validates so that the images have to live in the src directory and that they can only either be a PNG or JPEG file.

**Slots**

Use slots instead of prop based solution (usage of multiple props to achieve something)

Using slots can help avoid the unnecessary complexity from too many props:

```
**App.vue**
    <template>
        <main>
            <BaseButton>
                <AppIcon name="paperplane"/>
                Submit
                <AppIcon name="right-arrow"/>
            </BaseButton>
        </main>
    </template>

**BaseButton.vue**
    <template>
        <button class="button">
            <slot />
        </button>
    </template>

```

Slots are specialized elements in Vue that allows content similar to HTML to be passed.

All you have to do is declare the slot element inside the component. In order to delcare default values for a slot, simply define it in between the slot elements.

Giving a slot a name would be more precise and can be used to give elements directions as to while slot they fill up:

```
**component.vue**
    <template>
        <header>
            <slot name="header"></slot>
        </header>
        <main>
            <slot></slot>
        </main>
        <aside>
            <slot name="aside"></slot>
        </aside>
    </template>

**App.vue**
    <template>
        <component>
            <template v-slot:header>
                <h1>Title</h1>
            </template>
            <template v-slot:[slotName]>
                <p>Paragraph content</p>
            </template>
            <template v-slot:sidebar>
                <ul>
                    <li>number 1</li>
                    <l1>number 2</l1>
                </ul>
            </template>
        </component>
    </template>

```

Use template element to break the component into blocks. Add a v-slot directive and give it an arguement of the slot name that you want to pass information to.

When slot names need to be programmatically set, use "[slotName]", where "slotName" is a variable.

If a section is not given an explicit name, by default it would go into whatever slot is leftover (and it would be given the name of "default").

**Shorthand for v-slot**: #

```
<template #header></template>
```

:exclamation: The v-slot direction should only be used on template elements. :exclamation:
