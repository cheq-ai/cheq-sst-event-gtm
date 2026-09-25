# CHEQ Manage - Server-Side Tagging (SST) - Event template for Google Tag Manager

This Google Tag Manager (GTM) custom tag template sends events to your CHEQ Server-Side Tagging (SST) instance. Create one tag per event you want to track (e.g., page view, add to cart, purchase) and attach event data, custom data, and custom request parameters.

> **Note:** This template requires the SST Web SDK on the page. Load it with the [*CHEQ Manage - Server-Side Tagging - Web SDK*](https://tagmanager.google.com/gallery/#/owners/cheq-ai/templates/cheq-sst-sdk-gtm) template (typically on an **All Pages** trigger). Events pushed before the SDK loads are queued and sent once it initializes.

## Installation

**From the Community Template Gallery (recommended):**

1. In your GTM web container, go to **Templates > Tag Templates > Search Gallery**.
2. Search for **CHEQ** and add the [*CHEQ Manage - Server-Side Tagging - Event*](https://tagmanager.google.com/gallery/#/owners/cheq-ai/templates/cheq-sst-event-gtm) template.
3. Create a new tag from the template for each event you want to track and configure it (see below).

**Manual import:** download `template.tpl` from this repository, then in GTM go to **Templates > Tag Templates > New**, open the overflow menu, and choose **Import**.

## Configuration

| Field | Description |
|---|---|
| **Event Name** | The name of the event to trigger in the server-side instance (required). If it resolves to an empty value at runtime, e.g. from an unset GTM variable, the tag fails visibly instead of sending a nameless event. |
| **Event Data Object** | Optional variable that returns an object (e.g. an ecommerce object) to send as the event's data. If it doesn't return an object, the tag fails and no event is sent. |
| **Event Data** | Name/value pairs sent as the event's data, added on top of the Event Data Object (rows take precedence). A `__timestamp` field is added automatically unless you supply one. |
| **Send immediately** *(Options)* | If event batching is enabled in the Web SDK tag, send this event right away instead of batching it. |
| **Publish Path Override** *(Options)* | The publish path to send this event to. If left blank, the default publish path configured in the Web SDK tag is used. |
| **Custom Data** *(Options)* | Name/value pairs added to the SST event that may not be in your data layer; exposed as the `customData` variable within the SST browser. |
| **Custom Parameters** *(Options)* | Name/value pairs added to the SST request itself, such as `cw_xyz` for writing cookies to the browser. |

## How it works

The tag pushes the event onto the `Bootstrapper.SST` queue in the page (creating the queue if it doesn't exist yet; an existing `Bootstrapper` global is never overwritten). The SST Web SDK drains the queue and delivers the events to your SST instance.

## Documentation & support

- [Implementation with Google Tag Manager](https://help.ensighten.com/hc/en-us/articles/36258326811665-Implementation-with-Google-Tag-Manager)
- [CHEQ Manage](https://cheq.ai/manage/)

For help, contact CHEQ support through the [help center](https://help.ensighten.com/).

## License

Licensed under the [Apache License 2.0](LICENSE).
