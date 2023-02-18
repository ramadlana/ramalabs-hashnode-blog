# Add External Javascript Library for Svelte or SvelteKit

When we work with Javascript frameworks chances are we need to import external javascript for example importing template built-in js or maybe any legacy external javascript that you need to use on your App

Here are a few ways to import external js on SvelteKit

### Using {@html} decorator

For me, it's commonly used to import js template files and put them on `+layout.svelte`

```javascript
</div>
...
	{@html '<script src="/tabler.min.js"></script>'}
...
</div>
```

### Using svelte head

its mainly used if we want to import external js files and we wanna call a function after these external js loaded to DOM

First let see what our code if we code using vanilla js

```javascript
// Form
<form id="payment-form">
     ... your form things
</form>

<script src="https://js.stripe.com/v3/"></script>
// Create a Stripe client.
var stripe = Stripe('ourkeysecret1234567789zzz');

// Create an instance of Elements.
var elements = stripe.elements();
```

lets convert that to SvelteKit Components.

```javascript
<script>
    import { onMount } from 'svelte';
        let stripeReady = false;
        let mounted = false;
     
        onMount(() => {
            // onMount always call after Components mounted.
            mounted = true;
            // if stripe altready mounted load stripe element imediately
            if (stripeReady) {
                loadStripeElements();
            }
        });
 
        function stripeLoaded() {
            // if stripeReady -> load Stripe Element.
            stripeReady = true;
            if (mounted) {
                loadStripeElements();
            }
        }
 
        function loadStripeElements() {
            // create stripe elements
            const stripe = tripe('ourkeysecret1234567789zzz');
            var elements = stripe.elements();
            // etc..
        }
    }
</script>

<svelte:head>
    <script src="https://js.stripe.com/v3/" on:load={stripeLoaded}</script>
</svelte:head>

<div>
    <form id="payment-form">
         ... your form things
    </form>
</div>
```

That is. we successfully added an external (legacy) JS library into our Svelte Components.