#PolymerCounter

I was really struggling with Polymer 1.0 and the firebase-element. I wasn't having any issues with pulling data from Firebase, I was having issues with updating data in Firebase. I created this sample application to show how you can click on a div and have it update a counter.

The key to getting this to work was using:
```javascript
this.set('whatever', whatever);
```

Here's the full example:
```html
<firebase-collection location="whateverlocation" data="{{users}}"></firebase-collection>
<template is="dom-repeat" items="{{users}}">
    <div on-tap="levelUp">
        <span>{{item.name}}</span> - <span>{{item.level}}</span>
    </div>
</template>
```

```javascript
Polymer({
    is: 'counter-app',

    levelUp: function (event) {
        event.model.item.level += 1;
        this.set('users.' + event.model.index, event.model.item);
    }
});
```

Notice that to update the specific user in the users array, I need to use dot syntax instead of users[event.model.index]. Array syntax notation is not supported. Refer to the [Data binding](https://www.polymer-project.org/1.0/docs/devguide/data-binding.html) section of the Developer Guide if you need more information.
