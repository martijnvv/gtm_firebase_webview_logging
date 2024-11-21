# Firebase webview logging GTM template

This Google Tag Manager template allows you to easily configure the parameters to want to send to Firebase through the logEvent function.
The template allows you to include event data as well as user properties.

In order for this template to work, there are several steps to take:
1. Have the Firebase SDK running in the native app(s)
2. Include the native SDK webview handler in the native app(s)
3. Include the javascript handler in GTM or as part of the webview environment
4. Trigger events from GTM with the new logEvent custom GTM template you find here

## 1. Have the Firebase SDK running in the native app(s)

In order for data to be collected in your app (native or webview), you should implement the Firebase SDK in your native app environment

## 2. Have the Firebase SDK running in the native app(s)

You need to update the Firebase SDK (or let you app developers do this) by following the instructions outlined in the section "Implement native interface" in [the official Firebase documentation](https://firebase.google.com/docs/analytics/webview?platform=android#implement_native_interface).

## 3. Include the native SDK webview handler in the native app(s)

In your GTM client side container, add the Javascript Handles in a Custom HTML tag. The javascript function you create is called logEvent. The custom HTML tag should be populated with the code outlined in the [official Firebase documentation](https://firebase.google.com/docs/analytics/webview?platform=android#implement-javascript-handler) in the section called "Implement JavaScript handler". I generally trigger this javascript handler on initialization of the page, but only when the app version of a page is loaded. The last part basically excluded the tag from loading on the regular webiste version of the page, if this is applicable.

## 4. Trigger events from GTM with the new logEvent custom GTM template you find here

1. First download the  the template.tpl file and import it in your GTM container by navigating to GTM -> Templates - Tag Templates - New -> Import (right top corner) and save the template
2. Create a new tag and select the template "Firebase Analytics - Log webview events"
3. Now it's time to populate the template

### Configure the template

1. The Event name will reflect the name of the event you want to use in Firebase Analytics / GA4 (apps).

For e-commerce events, the event names are exactly the same for Firebase as they are for GA4.

2. Select the type of event you want to send to the app from the webview screen

Select Standard for any event non e-commerce (ie button click, page_view, etc)

3. Tick the box "Add Event Parameters" if you want to send any data to Firebase besides the event name.

Recommended parameters for any event would be screen_name and screen_class. Any other parameters are also accepted. You can map any event parameters that you have available in GTM to include them in you events.

4. Tick the box "Add User Properties" if you have any user properties to include in the event

Follow the same process as the event parameters

5. In the section "Developer settings", tick the box "Enable Console Logs" in case you want to see responses in the GTM debugger

### E-commerce tracking

E-commerce events work similar to standard events, with a few exceptions:

* Select E-commerce as type of events to track
* Tick the boxes of events you wish to track from the "Ecommerce Events" list
* By ticking these boxes, the items array is automatically included to the events. When selecting select_promotion and/ or view_promotion, the items array (if used for promotion data) is automatically flattened and used to trigger events for promotions. This also means that if you have multiple items in your view_promotion items array, an event is triggered for each item
* In addition to the items array, include additional event parameters you wish to send to the app. This also includes variables like transaction_id, value, etc. None of the standard variables are automatically included
* Just like standard events, you also have the option to include user properties to e-commerce events
