# -API-and-Payment-gateway
const stripe = require('stripe')('YOUR_SECRET_KEY_HERE'); // Use the 'sk_test...' key from your screen
const express = require('express');
const app = express();

app.post('/create-checkout-session', async (req, res) => {
  const session = await stripe.checkout.sessions.create({
    line_items: [{
      price_data: {
        currency: 'usd',
        product_data: { name: 'T-shirt' },
        unit_amount: 2000, // Amount in cents ($20.00)
      },
      quantity: 1,
    }],
    mode: 'payment',
    success_url: 'https://your-site.com',
    cancel_url: 'https://your-site.com',
  });

  res.redirect(303, session.url);
});

app.listen(4242, () => console.log('API is running!'));
