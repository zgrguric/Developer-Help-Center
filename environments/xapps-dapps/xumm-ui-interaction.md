---
description: >-
  Using the Xumm SDK in xApps, you can trigger native Xumm interaction & receive
  events from Xumm in your xApp.
---

# Xumm UI interaction

xApps are WebApps. They are opened in Xumm for a great user experience. They add value (tooling, wizards) for end users, using Sign Requests to help users perform tasks on the XRPL.

To add value for end users, your xApp will most likely implement some of the features Xumm offers natively in your xApp. E.g. open the QR scanner, Account Destination Picker, or start a Sign Request flow. Then to receive the response from these native Xumm flows in your xApp (WebApp).

**Your xApp can trigger specific actions in Xumm:**

These actions can be sent form your xApp (frontend Javascript) context, and will trigger functionality native to the Xumm app:

* Open a Sign Request
* Open the QR scanner to retrieve a scanned value
* Open the Account Destination Picker
* etc.

{% hint style="info" %}
To prevent showing a double loader (first the Xumm xApp loader, then your xApp's loader while hydrating / booting) you can enable the "**Xumm Loader Screen**" option in the Xumm Developer Console (xApp tab). See [ready.md](../../js-ts-sdk/sdk-syntax/xumm.xapp-.../ready.md "mention")
{% endhint %}

**Your xApp can also receive events (data) from Xumm:**

Certain actions in Xumm will trigger an event so your xApp can retrieve data or act based on the event (details below):

* Payload resolved
* QR Code scanner opened/closed
* Destination picker: closed / destination picked

## Example code

```html
<html lang="en">
  <body>
    <div id="destinationname">...</div>
    <input id="destinationaddress" value="" placeholder="Destination address" />
    <button onclick="xumm.xapp.selectDestination()">Pick destination account</button>

    <script src="https://xumm.app/assets/cdn/xumm.min.js"></script>
    <script>
      var xumm = new Xumm('your-api-key')

      xumm.xapp.on('destination', data => {
        if (data.destination.address) {
          document.getElementById('destinationname').innerText = data.destination.name
          document.getElementById('destinationaddress').value = data.destination.address
        } else {
          console.log('No destination selected', data.reason)
        }
      })
    </script>
  </body>
</html>
```

## Trigger actions

{% hint style="info" %}
For all Xumm UI (interface) actions / worfklows you can trigger, see the SDK documentation: [xumm.xapp-...](../../js-ts-sdk/sdk-syntax/xumm.xapp-.../ "mention")
{% endhint %}

## Receive events

{% hint style="info" %}
For all events emitted in your xApp (like the async follow up data of an xApp UI action triggered), see the xApp event handler: [on-event-fn.md](../../js-ts-sdk/sdk-syntax/xumm.xapp-.../on-event-fn.md "mention")
{% endhint %}
