#Available Hooks
###beforeCreate
- is called before instance initialization
- Data changed; update pending
### Updated
- Re-rendered to reflect changes
###beforeDestroy
- vm.$destroy()called
###Destroyed
- Watchers and event handlers removed no reactivity
###Created
- Is called after the properties are configured but before instance has been mounted to the dom.
(Reactive properties configured; instance not yet mounted)
###beforeMount
-Template compiled; ready to be inserted in DOM
###Mounted
-Template inserted in DOM, replacing 'el' element
