#Customising the Dashboard

Hygieia uses the CSS framework Bootstrap 3. This document will explain how to customise Hygieia with custom branding, using SECTION6 branding as an example. For comprehensive customisation of the dashboard, see the [Bootstrap 3 documentation](https://getbootstrap.com/docs/3.4/customize/). 



##Before you start

To test your changes, you can run just the UI code by navigating to `Hygieia/UI` and running the following command:
```
gulp serve --local true
```

Whenever a change is made to the frontend code, it will refresh the page with the new changes. 

###Add custom images

You will need the following images:

* A logo for light background
* A logo for dark background
* An avatar logo for smaller screens
* A background image

Place these in the `Hygieia/UI/src/assets/img/` directory.

###Create custom theme file

In this example we will be extending the existing "dash" theme used by Hygieia. 

Create a new .less file in `UI/src/components/themes/`. In this case we will call it `section6.less`. Copy everything from `dash.less` into this file.

Go to `UI/src/app/app.js` and set the theme to your new theme file, e.g:
```
    // set default theme
    var theme = 'section6';
```

Now run `gulp serve --local true`. It should look the same, as we haven't made any changes to the default theme yet. 

#####Import brand colors

Above the `// LOCAL VARIABLES FOR THIS THEME` line, define your branding colors. For this example we will use the SECTION6 colors:

```
//Import brand colors
@s6-dark-purple: #32243F;
@s6-purple-1: #61166D;
@s6-purple-2: #8C288B;
@s6-dark-grey: #272626;
@s6-black: #000000;
@s6-white: #FFFFFF;
```

#####Add custom logo URLs

Add the following definitions to override the logo URLS. Adjust the file names, size and position variables as needed:

```
//Logo definitions
//===========================================
// Header logo
@dash-header-logo-url: '@{dash-image-path}section6-logo-white.png';
@dash-header-logo-width:            135px;
@dash-header-logo-height:           35px;
@dash-header-logo-left:             10px;
@dash-header-logo-top:              8px;
@dash-header-logo-inverse-url: '@{dash-image-path}section6-logo-dark.png';
// Logo for smaller screens
@dash-header-icon-url: '@{dash-image-path}section6-avatar.png';
@dash-header-icon-width:            41px;
@dash-header-icon-height:           48px;
@dash-header-icon-left:             60px;
@dash-header-icon-top:              10px;
```

#####Override color scheme

Overriding the colors involves a lot of trial and error. It is especially tricky if you want to change the background color from light to dark (as we will do in this example), as it means you need to change the text colors as well to ensure it is still readable. 

######BOOTSTRAP VARIABLES section
Under "Bootstrap variables", update the following values. These will change the color of the various buttons on the site:
```
@btn-primary-bg: @s6-purple-1;
@btn-default-bg: @s6-purple-2;
@btn-primary-border: @btn-primary-bg;
@btn-default-border: @s6-purple-2;
...
@btn-info-bg: @s6-purple-2;

//Navbar colors
@navbar-default-bg: @white;
@navbar-inverse-bg: @s6-dark-grey;
@navbar-inverse-border: @navbar-inverse-bg;
```


######BOOTSTRAP OVERRIDES section
Delete the entire "Bootstrap Overrides" section, or if you wish, update the values in these overrides with your theme colors. The existing values here change the appearance of the buttons. 

######DASH VARIABLES section
Under "Dash Variables", add and update the following values:

```
//Background and text color
@dash-bg: @s6-dark-purple;
@dash-text: @s6-white;
@dash-dashboard-text: @s6-white;

...

//Various modal elements, switching from light to dark theme
@dash-modal-bg: @s6-dark-purple;
@dash-modal-heading-text: @dash-text;
@dash-modal-heading-border: rgba(255, 255, 255, .35);
@dash-modal-divider: rgba(255, 255, 255, .25);
@dash-modal-icon-text: rgba(255, 255, 255, .5);
```

######SITE section
Update the `#site {}` entry with the following. This will change the colors of the list of dashboards on the front page. Here we are making them purple, with a brighter purple on hover:

```
#site {
    .list-group-item {
        background-color: @s6-purple-1;
    }
    .list-group-item:hover {
        background-color: @s6-purple-2;
    }
}
```

######DASHBOARD section
Update the background-image path to point to your own. This background doesn't appear on the front page, it shows up when you click on a particular dashboard:
```
#dashboard {
    background-image: url('@{dash-image-path}bg-section6.jpg');
```

