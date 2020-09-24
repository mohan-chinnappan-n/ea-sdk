# Einstein Analytics SDK

- Analytics SDK lets you communicate and interact with Analytics assets from Lightning Apps, Apex, Visualforce, and more.
- You can access the power of REST APIs to retrieve collections of Analytics assets, such as dashboards, lenses, and datasets and describe the details of individual assets. 
    - Customize the display of the results via a Lightning Component controller.
    - Create dynamic SAQL queries against your Analytics data to display runtime results.

- Analytics Web SDK Events
    - Lets your application to communicate with your Analytics dashboards, whether your application is built with the Lightning SDK, Visualforce, or mobile
    - Your application could apply filters or know about *dashboard selections and filters* made by a user 

- Analytics Apex SDK
    -  Allows to  query data in Analytics directly from your Apex code
    -  Lets developers build SAQL queries and execute them in the security context of the logged-in user,


<a name='websdk'></a>
## Analytics Web SDK Events
- **wave:assetLoaded**
    - After this event is received, you can safely reapply mandatory filters or resync the dashboard state.
- **wave:update**
    - dynamically set the **filter** on an Analytics dashboard or interact with the dashboard by dynamically changing the selection.
    - 4 attributes
        1. unique ID of the Analytics asset on which to apply the filter, 
        2. the payload, 
            - The payload is a JSON string that identifies the datasets and any dimensions and field values.
        3. the asset type (currently only dashboard), 
        4. fully qualified developer name of the Analytics dashboard. 
- **wave:selectionChanged**
    -  fires this event for consumption by custom Aura components
    -  provides attributes
        1. the ID of the dashboard that fired the event 
        2. the payload.
            -  The payload object contains the selection information
                — the name of the step involved when changing the selection 
                - an **array of objects** representing the current selection. 
                    - Each object in the array contains one or more attributes based on the selection.
        - [Analytics Web SDK Events - SelectionChanged Event](https://developer.salesforce.com/docs/atlas.en-us.bi_dev_guide_sdk.meta/bi_dev_guide_sdk/bi_sdk_web_example2.htm)
```js
({
  handleSelectionChanged: function(component, event, helper) {
    var params = event.getParams();
    var payload = params.payload;
    if (payload) {
      var step = payload.step;
      var data = payload.data; // array representing the current selection.
      data.forEach(function(obj) {
        for (var k in obj) {
          if (k === 'Id') {
            component.set("v.recordId", obj[k]);                        
          }
        }
      });
    }
  }
})
```
    - The dashboard component generates Lightning events when the user changes a selection
```xml
<aura:component implements="force:appHostable,
                flexipage:availableForAllPageTypes,
                flexipage:availableForRecordHome,
                force:hasRecordId,
                forceCommunity:availableForAllPageTypes,
                force:lightningQuickAction"
                access="global" >
  <aura:handler event="wave:selectionChanged" action="{!c.handleSelectionChanged}"/>
  <aura:attribute name="msg" type="String" default="Please make a selection in Analytics that contains a record ID" access="GLOBAL"/>
  <aura:attribute name="recordId" type="String" default="" access="GLOBAL"/>
  <aura:dependency resource="markup://force:navigateToSObject" type="EVENT"/>        
  <div class="container">
    <aura:if isTrue="{!v.recordId == ''}">
      <div class="msg">
        {!v.msg}
      </div>
      <aura:set attribute="else">
        <force:recordView recordId="{!v.recordId}"/> 
      </aura:set>
    </aura:if>
  </div>	
</aura:component>
```


- **wave:discover**
    - sends a global request to identify Analytics dashboard assets.
    -  response is a **wave:discoverResponse** event
        - fired by listening to Analytics dashboard assets in response to the **wave:discover** event.
            - Payload includes
                1. dashboard identifier, 
                2. the type of component, 
                3. the dashboard title, 
                4. whether the dashboard is still loading, 
                5. any optional parameter sent with the request
- **wave:discoverResponse**
    - Use this event to update the Analytics dashboard page that is displayed. 
    - has two attributes
        -  unique ID of the page to display
        - fully qualified developer name of the Analytics dashboard 
## Topics
- [References](#ref)



<a name='ref'></a>
- [Analytics SDK Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.bi_dev_guide_sdk.meta/bi_dev_guide_sdk/bi_sdk_overview.htm)
