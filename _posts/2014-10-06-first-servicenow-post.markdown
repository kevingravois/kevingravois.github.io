---
layout: post
title:  "First ServiceNow Post"
date:   2014-10-06 20:43:00
categories: servicenow
---

This is a post regarding ServiceNow that will display some sample JavaScript code.

{% highlight javascript %}
// For support of warning when two people are editing the same record.
 function onSubmit() {
   var updatedOn = gel('onLoad_sys_updated_on');
   if (!updatedOn)
      return;
 
   updatedOn = updatedOn.value;
   if (!updatedOn)
      return;
 
   var sysid_gel = gel('sys_uniqueValue');
   var sysid = sysid_gel.value;
   var gr = new GlideRecord('incident');
   gr.addQuery('sys_id',sysid);
   gr.query();
   if (gr.next()) {
      var dbUpdatedOn = gr.sys_updated_on + '';
      var dbUpdatedBy = gr.sys_updated_by + '';
   } else
      return;
 
   if (updatedOn != dbUpdatedOn) {
      return confirm("Record has been updated by " + dbUpdatedBy + " since you opened it - "
      + "overwrite those changes with yours? Note that Additional comments and Work notes are "
      + "additive and will not be overwritten.");
   }
 }
{% endhighlight %}
