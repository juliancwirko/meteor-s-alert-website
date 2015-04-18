## Installation

**Note: From version 2.0.0 you should also choose and add effect package.**
This is more elastic and optimal solution (effects css file contained all effects styles and it was heavy). It will work without effects too. You can add as many effect packages as you want. Config and usage is the same.

<p>&nbsp;</p>

**Add package:**

    meteor add juliancwirko:s-alert

<p>&nbsp;</p>

**Or/And add it with one of effects:**

    meteor add juliancwirko:s-alert-scale
    meteor add juliancwirko:s-alert-slide
    meteor add juliancwirko:s-alert-genie
    meteor add juliancwirko:s-alert-jelly
    meteor add juliancwirko:s-alert-flip
    meteor add juliancwirko:s-alert-bouncyflip
    meteor add juliancwirko:s-alert-stackslide

## Demo

[http://s-alert-demo.meteor.com/](http://s-alert-demo.meteor.com/)

## Usage

Then place ````{{> sAlert}}```` in your main template. Recomended usage:

    <body>
        {{> sAlert}}
    </body>

### sAlert configuration

You can set up your sAlert (client side). (More about possible configuration options below.) You can ommit it and you will have standard config which is the same as the one below:

    Meteor.startup(function () {

        sAlert.config({
            effect: 'scale',
            position: 'right-top',
            timeout: 5000
        });

    });

sAlert is based on only client side collection. It is called ````sAlert.collection````

### Fire up your alerts by using methods:

#### Error:

    sAlert.error('Your message', configOverwrite);

#### Warning:

    sAlert.warning('Your message', configOverwrite);

#### Info:

    sAlert.info('Your message', configOverwrite);

#### Success:

    sAlert.success('Your message', configOverwrite);

#### Close alert:

    sAlert.close(allertId);
- id is from Meteor collection called ````sAlerts.collection```` (client only)

#### Immediately close all alerts:

    sAlert.closeAll();


And what is ````configOverwrite````?
This is an object with all settings which you want to overwrite. So if you have your sAlert config (mentioned above) you can overwrite global config with each of your sAlert calls.

**For example:**

    sAlert.error('Boom! Something went wrong!', {effect: 'genie', position: 'right-bottom', timeout: 'no'});

This one particular error will be displayed in different way.

### Avaible effects:

- **scale** ( <small>`meteor add juliancwirko:s-alert-scale`</small> )
- **slide** ( <small>`meteor add juliancwirko:s-alert-slide`</small> )
- **genie** ( <small>`meteor add juliancwirko:s-alert-genie`</small> )
- **jelly** ( <small>`meteor add juliancwirko:s-alert-jelly`</small> )
- **flip** ( <small>`meteor add juliancwirko:s-alert-flip`</small> )
- **bouncyflip** ( <small>`meteor add juliancwirko:s-alert-bouncyflip`</small> )
- **stackslide** ( <small>`meteor add juliancwirko:s-alert-stackslide`</small> ) (right-top and left-top positions are the same here similar right-botton and left-bottom)

### Avaible positions:

- left-top
- left-bottom
- right-top
- right-bottom

### Timeout:

You can set up it in miliseconds or place 'no'.

## CSS styling

You can overwrite all css classes. Major classes which are defined by conditions are:

- .s-alert-blue
- .s-alert-green
- .s-alert-yellow
- .s-alert-red`

For example if you want to overwrite .s-alert-red in scale effect

```css
.s-alert-effect-scale.s-alert-red {
    background: #bada55; //your background color here
    color: #fff //your text color here
}
```

## Your own effects packages

You can prepare your own effect package. As a reference take one of the ready to use packages. You will find the code on GitHub. You can create your own animations, but remember to use `.s-alert-effect-{your-effect-name-here}` prefix. Then you can use it like:

```
sAlert.error('Boom! Something went wrong!', {effect: 'your-effect-name-here', position: 'right-bottom', timeout: 'no'});
```

Or you can place it in the config:

```
Meteor.startup(function () {

    sAlert.config({
        effect: 'your-effect-name-here',
        position: 'right-top',
        timeout: 5000
    });

});
```
If you want to have your effect package linked here just let me know.

## Template overwriting

Here is a default template (it will be included when you use standard ````{{> sAlert}}````):

    <div class="s-alert-box s-alert-effect-{{effect}} s-alert-{{condition}} s-alert-{{position}} s-alert-show" id="{{_id}}">
        <div class="s-alert-box-inner">
            <p>{{message}}</p>
        </div>
        <span class="s-alert-close"></span>
    </div>

If you want to owerwrite it you should remember to be careful with all used helpers. They should remain in place.
**Here you have an example of overwriting an alert content template** (Place it somewhere in your html files, you can name it as you want):

    <template name="sAlertCustom">
        <div class="my-custom-alert-class s-alert-box s-alert-effect-{{effect}} s-alert-{{condition}} s-alert-{{position}} s-alert-show" id="{{_id}}">
            <div class="s-alert-box-inner">
                <div class="alert-header">
                    <h1>{{sAlertTitle}}</h1>
                </div>
                <div class="alert-content">
                    <i class="fa fa-fw fa-cog"></i>
                    {{message}}
                </div>
            </div>
            <span class="s-alert-close"></span>
        </div>
    </template>

### Usage of custom template

Place

```
{{> sAlert template='sAlertCustom'}}
```

in your main template.

## Custom fields

As you can see in a custom `sAlertCustom` template we have used `sAlertTitle` custom helper. Now if you want to pass the value to it you should call one of sAlert functions with first param as an object instead of a message string. See example:

```
sAlert.info({sAlertTitle: 'My custom sAlert field - the title', message: 'My sAlert message here'}, configOverwrite);
```
You can pass as many fields as you like. Remember to add the corresponding helpers in template. `configOverwrite` works here the same as described above. It is of course optional.

### Using with routers:

If you go to another route it should autoclean alerts. Works with Iron Router and FlowRouter.
If you notice any bugs related with this please drop me a note. Thanks.

### Inspiration:

- [Codrops Article - Notification Styles Inspiration](http://tympanus.net/codrops/2014/07/23/notification-styles-inspiration/)

### License

MIT

### Download and use this website for your documentation

```
$ git clone https://github.com/juliancwirko/meteor-s-alert-website.git
$ cd meteor-s-alert-website
$ rm -rf .git
$ meteor
```
[https://github.com/juliancwirko/meteor-s-alert-website](https://github.com/juliancwirko/meteor-s-alert-website)

### Check out other tools for Meteor:

* [Prettify and export your raw git diff output](https://atmospherejs.com/juliancwirko/pretty-diff)
* [Foundation 5 with Scss for Meteor](https://atmospherejs.com/juliancwirko/zf5)
* [Stylus, Flexbox grid system](https://atmospherejs.com/juliancwirko/s-grid)
* [Stylus with Jeet, Autoprefixer, Rupture and Nib for Meteor](https://atmospherejs.com/juliancwirko/s-jeet)
* [Simple accounts for Meteor](https://atmospherejs.com/juliancwirko/s-id)
* [Scotty - Meteor boilerplate](https://github.com/juliancwirko/scotty)
* [Meteor CylonJS wrapper for Arduino board](https://atmospherejs.com/juliancwirko/caprica)

### Also check out standalone front-end tools:

* [S-Grid (Stylus, Flexbox grid) GruntJS project scaffold](https://github.com/juliancwirko/s-grid-grunt)
* [Yeoman generator for Zurb Foundation 5](https://github.com/juliancwirko/generator-zf5)
* [Free, very simple and clean starter theme for your Ghost blog](https://github.com/juliancwirko/abc)
* [HTML only and GruntJS based project scaffold](https://github.com/juliancwirko/html-project)