# Connecting with Salesforce

In order to make calls against the Salesforce Rest API you need to provide ts-force with an `accessToken` and an `instanceUrl` .  How you obtain the access token is left up to you.  `ts-force` does provide some functions for obtaining access tokens for common oAuth flows.

## Default vs Instance Connections

### Default Connection

If you are only working with a **single connection with straight-forward use cases** you might find it more convenient to set the "default" configuration:

{% tabs %}
{% tab title="setup.ts" %}
```typescript
import { setDefaultConfig } from 'ts-force';

setDefaultConfig({
   accessToken: 'abc123',
   instanceUrl: 'https://na3.salesforce.com'
});
```
{% endtab %}

{% tab title="doSalesforceStuff.ts" %}
```typescript
import { Rest, CompositeCollection } from 'ts-force';

//all of these are automatically setup with the default connection
const client = new Rest();
const collection = new CompositeCollection();
const myAccount = new Account();
```
{% endtab %}
{% endtabs %}

### Multiple \(Managed\) Connections

If you need more control or or using multiple salesforce orgs then you'll need to explicitly setup `Rest` clients.

{% code title="doSalesforceStuff.ts" %}
```typescript
import { Rest } from 'ts-force';

const restInstance = new Rest({
   accessToken: 'abc123',
   instanceUrl: 'https://na3.salesforce.com'
});

const secondaryRestInstance = new Rest({
   accessToken: 'abc123',
   instanceUrl: 'https://na3.salesforce.com'
});

//create a collection client for the primary connection
const collection = new CompositeCollection(restInstance);

// account connected to primary instance
const primaryAcc = new Account({name: 'foo'}, restInstance);

//query accounts on the secondary instance
const secondaryAcc = await Account.retrieve(f => ({
  select: ['name'],
  limit: 1
}), {restInstance: secondaryRestInstance});
```
{% endcode %}

## I already have an access token

If you already have an access token, you can simply create a new Rest Instance

```typescript
const
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}


